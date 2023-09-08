# Instalação dal libs
```sh
    pip install request beautifulsoup4
```

# Scrapping
```py
    from bs4 import BeautifulSoup
    import requests

    html = requests.get("https://www.climatempo.com.br/").content

    soup = BeautifulSoup(html, 'html.parser')

    print(soup.prettify())
```

## Get temperatura mínima e máxima
```py
    temperatura = soup.find("span", class_="_block _margin-b-9 -gray")
    print(temperatura.string)
```

---

# REFERÊNCIAS
[Como Fazer Um Web Scrapping](https://blog.geekhunter.com.br/como-fazer-um-web-scraping-python/#O_que_e_web_scraping)
