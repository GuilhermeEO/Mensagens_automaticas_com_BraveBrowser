# Mensagens_automaticas_com_BraveBrowser
#Automação com Selenium e Pandas para o Whatsapp, usando Python


import pandas as pd

contatos_df = pd.read_excel("Enviar.xlsx")

#display(contatos_df)

from selenium import webdriver

from selenium.webdriver.common.keys import Keys

import time

import urllib

#navegador = webdriver.Chrome()

option = webdriver.ChromeOptions()

option.binary_location = 'C:/Program Files/BraveSoftware/Brave-Browser/Application/brave.exe'

navegador = webdriver.Chrome(executable_path='C:/Users/win/AppData/Local/Programs/Python/Python38-32/chromedriver.exe', options=option)

navegador.get("https://web.whatsapp.com/")

while len(navegador.find_elements_by_id("side")) < 1:
    time.sleep(1)

for i, mensagem in enumerate(contatos_df['Mensagem']):

  pessoa = contatos_df.loc[i, "Pessoa"]
    
  numero = contatos_df.loc[i, "Número"]
    
  texto = urllib.parse.quote(mensagem)
    
  link = f"https://web.whatsapp.com/send?phone={numero}&text={texto}"
    
  navegador.get(link)
    
  while len(navegador.find_elements_by_id("side")) < 1:
      time.sleep(1)
        
  #navegador.find_element_by_xpath('//*[@id="main"]/footer/div[1]/div/span[2]/div/div[2]/div[1]/div/div[2]').send_keys(Keys.ENTER)
  #Em alguns "Braves" o Enter automático não funciona em todos os chats, opte por enviar manualmente em cada tela com o Enter
    
  time.sleep(10)



