# YouTubePars
import telebot
from selenium import webdriver


driver = webdriver.Edge()

bot = telebot.TeleBot("")

@bot.message_handler(commands=['start'])
def start(message):
    bot.send_message(message.chat.id, "Приветствую")

@bot.message_handler(commands=['search_videos'])
def search_videos(message):
    msg = bot.send_message(message.chat.id, "Введите текст,который вы хотите найти в YouTube")
    bot.register_next_step_handler(msg, search)

@bot.message_handler(content_types=['text'])
def text(message):
    bot.send_message(message.chat.id, "Ты что-то хотел?")
def search(message):
    bot.send_message(message.chat.id, "Начинаю поиск")
    video_yout = "https://www.youtube.com/results?search_query=" + message.text
    driver.get(video_yout)




bot.polling()
