import logging
import random
import time
from datetime import datetime, timedelta
import telebot

logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')
logger = logging.getLogger(__name__)

bot = telebot.TeleBot(6234570700:AAGhn0AgyOukbk9JiK4xWtD0nc1vIJCQVz0)

grupo_id = -1002067234753


admins_ids = [5587769057, 5587769057]

manutencao_ativa = False
mensagem_manutencao = None

mensagem_sinal_atual = None

def enviar_sinal(destino_id):
    minas = random.choice([3, 4])
    hora_validade = datetime.now() + timedelta(minutes=5) 

    current_time = time.strftime("%H:%M:%S", time.localtime())
   
    tabuleiro = [['⚫️' for _ in range(5)] for _ in range(5)]

    estrelas = random.sample(range(25), minas)

    for posicao in estrelas:
        linha = posicao // 5
        coluna = posicao % 5
        tabuleiro[linha][coluna] = '💎'

        mensagem = f"O sistema gerou os seguites\n\n"
        mensagem += f"*Aposte com* : {minas} 💣.\n\n"
        mensagem += '\n'.join([''.join(linha) for linha in tabuleiro])
        mensagem += "\n\n🎯 Use até 2 gales\n"
        mensagem += f"⏰ Validade até às *{hora_validade.strftime('%H:%M')}*\n"
        mensagem += "🎯PLATAFORMA: "


    global mensagem_sinal_atual
    mensagem_sinal_atual = bot.send_message(canal_id, mensagem, parse_mode='Markdown')

    agendar_novo_sinal(hora_validade, canal_id)

def agendar_novo_sinal(hora_validade, canal_id):
    agora = datetime.now()
    tempo_restante = hora_validade - agora

    time.sleep(tempo_restante.total_seconds())
    enviar_sinal(canal_id)

    remover_sinal_anterior(canal_id)


if __name__ == '__main__':
    logger.info("Bot iniciado com succesu")
    enviar_sinal(grupo_id)
    enviar_sinal(can
    al_id)
bot.polling()
