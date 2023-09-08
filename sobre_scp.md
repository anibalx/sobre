# OBS: ações realizadas a partir da máquina cliente: ENVIA e BUSCA.


# ENVIA: Arquivo do cliente para o servidor
scp nome_do_arquivo_a_ser_enviado.txt user_server@hostname:/home/$USER
 ex: scp arquivo.txt fabio@192.168.1.189:~
     password: senha do usuário no servidor ("user_server")


# BUSCA: Arquivo do servidor para cliente
scp user_server@hostname:caminho_do_arquivo nome_que_o_arquivo_receberá_na_minha_máquina
 ex: scp fabio@192.168.1.189:/home/fabio/servidor veio_do_servidor.txt
     password: senha do usuário no servidor ("user_server")

     OBS: ao especificar o nome do arquivo a ser buscado,
	  pode-se passar apenas seu nome, 
	  dado sua existência na pasta do "user_server":
		ex: scp fabio@192.168.1.189:servidor veio_do_servidor.txt

