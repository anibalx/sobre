# Habilita docker
```
systemctl enable --now docker
```  

# Criação de um projeto mix localmente ligado ao container
Usamos então a opção -v local_path:container_path, onde ambos os caminhos precisam ser absolutos. Vamos tentar criar um novo projeto de elixir usando `mix new` e ligar a montagem de um diretório local.

```sh
docker container run --rm -v $PWD:/data -w /data elixir:1.7.4 mix new crypto
```



# Extrutura do projeto mix criado localmente
Nós montamos o diretório atual no caminho de /data do container, usando a variável de ambiente `$PWD`. Também adicionamos uma opção -w /data que diz ao container para iniciar o comando no diretório de trabalho /data. Podemos ver que o diretório crypto está agora em nosso diretório atual. Mix.exs

```sh
└── crypto
    ├── lib
    │   └── crypto.ex
    ├── mix.exs
    ├── README.md
    └── test
        ├── crypto_test.exs
        └── test_helper.exs
```



# inserção de dependência localmente 
Vamos mover para dentro do diretório cripto 
```sh
cd crypto
```

e adicionar uma dependência em mistura. exs
```ex
defp deps do
  [ {:poison, "~> 4.0"} ]
end
```

## comando para inserção de dependência
```sh
docker container run --rm -v $PWD:/app -w /app -it elixir:1.7.4 mix deps.get
```

Não conseguiu encontrar Hex, que é necessário para construir dependência :poison
Devo instalar o Hex? (se estiver executando de forma não interativa, use "mix local.hex --force") [Yn] Y.



# crição de volume para
Depois que a dependência é baixada e construída, o container é destruído e todos os dados em /root/.mix está perdida. Se executarmos novamente os mesmos comandos teremos novamente de instalar o hex. Para resolver isso, um problema semelhante, podemos criar um volume local

```sh
docker volume create elixir-mix
```


## uso do volume criado
Para usá-lo, precisamos adicionar outra opção ao comando -v volume-name:container_mount_point.

```sh
docker container run --rm -v elixir-mix:/root/.mix -v $PWD:/app -w /app -it  elixir:1.7.4 mix deps.get # adição das dependências
docker container run --rm -v elixir-mix:/root/.mix -v $PWD:/app -w /app -it  elixir:1.7.4 mix deps.get # teste se as dependências foram adicionadas
```


# execução do iex com dependência instalada
A primeira vez, Hex precisa ser instalado. A segunda vez, o comando está funcionando corretamente porque o hex é encontrado no diretório /root/.mix, onde o volume elixir-mix é montado.

Agora podemos executar nosso iex carregando nosso projeto cripto

```sh
docker container run --rm -v elixir-mix:/root/.mix -v $PWD:/app -w /app -it  elixir:1.7.4 iex -S mix
iex(1)> Poison.encode! %{hello: :world}
```

As dependências são baixadas em deps e compiladas no diretório do projeto de build (compilação). 
Uma vez que essas mudanças são refletidas em nosso diretório de projeto 
através da montagem de vinculação, 
se executarmos o mesmo comando novamente 
não devemos ter nenhuma compilação de dependências



# Rode Multiplus Containers
- Cria rede
```
  docker network create elixir-net
```

- Inspeciona rede criada
```
  docker network inspect elixir-net
```

- Rode Elixir na rede recém criada
1. -it == rode em modo iterativo
2. --rm == remova container após execução
3. --network == rode nessa rede
```
  docker run -it --rm --network elixir-net elixir:1.7.4
```

- liste os containers rodando
```
  docker container ls
```

- Inspeciona o container e pegue o IP ADDRESS
1. jq == processe a saída como um JSON
```
  docker container inspect <CONTAINER_ID> | jq
```

- Rode Elixir na rede recém criada e utilize o bash
1. -it == rode em modo iterativo
2. --rm == remova container após execução
3. --network == rode nessa rede
```
  docker run -it --rm --network elixir-net elixir bash
```

## Terminal 1
- Rode Elixir na rede recém criada
1. -it == rode em modo iterativo
2. --rm == remova container após execução
3. --network == rode nessa rede
4. --name == rode nessa rede
5. -h == hostname do container
```
  docker run -it --rm --network elixir-net --name elixir-1 -h elixir-1 elixir bash
```

## Terminal 2
- Rode Elixir na rede recém criada
1. -it == rode em modo iterativo
2. --rm == remova container após execução
3. --network == rode nessa rede
4. --name == rode nessa rede
5. -h == hostname do container
```
  docker run -it --rm --network elixir-net --name elixir-2 -h elixir-2 elixir bash
```

- ping no terminal
```
  ping elixir-1 # ou coloque o IP ADDRESS
```

 
## Conexão entre as máquinas

## Terminal 1
- Rode Elixir na rede recém criada
1. -it == rode em modo iterativo
2. --rm == remova container após execução
3. --network == rode nessa rede
4. --name == rode nessa rede
5. -h == hostname do container
6. --sname == elixir -> nomeie o nó elixir
7. --cookie == elixir -> envio de uma "senha"
```
  docker run -it --rm --network elixir-net --name elixir-1 -h elixir-1 elixir iex --sname docker --cookie '$COOKIE'
```

- Após criar um Agent em "elixir-2", um "Agent.get" espera pegar uma informação advinda de "Agent"
```
 iex(docker@elixir-1)1> Agent.get({:global, MyAgent}, fn state -> state end)
 {:hello, :world}
```

## Terminal 2
- Rode Elixir na rede recém criada
1. -it == rode em modo iterativo
2. --rm == remova container após execução
3. --network == rode nessa rede
4. --name == rode nessa rede
5. -h == hostname do container
6. --sname == elixir -> nomeie o nó elixir
7. --cookie == elixir -> envio de uma "senha"
```
  docker run -it --rm --network elixir-net --name elixir-2 -h elixir-2 elixir iex --sname docker --cookie '$COOKIE'
```

- Liste as conexões realizadas ao nó "docker"
```
  iex(docker@elixir-2)1> Node.list
```

- Conexão do node "elixir-2" até o node "elixir-2"
```
  iex(docker@elixir-2)1> Node.connect :"docker@elixir-1"
```

- Criação de Agent dentro do "elixir-2"
```
 iex(docker@elixir-2)1> Agent.start_link(
 ...(docker@elixir-2)1> fn -> {:hello, :world} end,
 ...(docker@elixir-2)1> name: {:global, MyAgent})
 {:ok, #PID<0.119.0>}
```

# REFERÊNCIAS
[Running Elixir in Docker Containers](https://www.poeticoding.com/running-elixir-in-docker-containers)
