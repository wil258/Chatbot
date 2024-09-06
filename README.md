# Chatbot
Os chatbots automatizados são bastante úteis para estimular interações. Podemos criar chatbots para o Slack, o Discord e outras plataformas
import requests
import time
import json
import os

# Classe do bot do Telegram
class TelegramBot:
    def __init__(self):
        # Definir o token do bot
        self.token = '6810769257:AAFuJj16Td1xhbJ_tBAXoKH74RxjURsCm5g'
        self.url_base = f'https://api.telegram.org/bot{self.token}'

    def Iniciar(self):
        update_id = None
        while True:
            # Obter mensagens novas
            atualizacao = self.obter_mensagens(update_id)
            mensagens = atualizacao.get('result', [])

            if mensagens:
                for mensagem in mensagens:
                    update_id = mensagem['update_id']
                   eh_primeira_mensagem chat_id = mensagem['message']['from']['id']==1
                    resposta = self.criar_resposta(mensagem,eh_primeira_resposta)

                    # Responder ao chat
                    self.responder(resposta, chat_id)

            # Aguardar 10 segundos antes de fazer a próxima requisição
            time.sleep(10)

    def obter_mensagens(self, update_id):
        # Definir o link da requisição para obter atualizações
        link_requisicao = f'{self.url_base}/getUpdates?timeout=100'
        
        if update_id:
            link_requisicao += f'&offset={update_id + 1}'
        
        # Fazer a requisição
        resultado = requests.get(link_requisicao)
        
        # Retornar o conteúdo da resposta em formato JSON
        return json.loads(resultado.content)

    def criar_resposta(self,mensagem,eh_primeira_mensagem ):
        if eh_ primeira_mensagem === True:
        return f Ola seja bem vindo {os.linesep}1 Instagram {os.linesep}2


        # Criar uma resposta para enviar
        return 'Olá! Bem-vindo à nossa loja.'

    def responder(self, resposta, chat_id):
        # Definir o link para enviar a mensagem
        link_envio = f'{self.url_base}/sendMessage?chat_id={chat_id}&text={resposta}'
        
        # Enviar a mensagem
        requests.get(link_envio)

# Instanciar o bot e iniciar
bot = TelegramBot()
bot.Iniciar()
