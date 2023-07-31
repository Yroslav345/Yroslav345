- import telebot
import webbrowser
from telebot import types



bot =telebot.TeleBot("5893331690:AAGYktQkozUX4YxVu7CSHP5w8aCKXLk1cmY")

@bot.message_handler(commands=["site"])
def site(message):
    webbrowser.open("https://www.youtube.com/watch?v=ObwoMskHDoA&list=PL0lO_mIqDDFUev1gp9yEwmwcy8SicqKbt&index=1")







@bot.message_handler(commands=['start'])
def main(message):
    bot.send_message(message.chat.id, "ПРИВЕТ спасибо за  то что вы выбрали мой бот")

@bot.message_handler(commands=['Help'])
def main(message):
    bot.send_message(message.chat.id, "Help information, информации пока нет" )


@bot.message_handler()
def info(message):
    if message.text.lower() == "привет":
        bot.send_message(message.chat.id, "ПРИВЕТ спасибо за  то что вы выбрали мой бот")

    elif message.text.lower() == "id":
         bot.reply_to(message,"информация запрещена")

@bot.message_handler(content_types=["photo", "audio"])
def get_photo(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton("Перейти на сайт", url="https://www.youtube.com/watch?v=ObwoMskHDoA&list=PL0lO_mIqDDFUev1gp9yEwmwcy8SicqKbt&index=1"))

    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton("удалить фото",callback_data="delete"))
    markup.add(types.InlineKeyboardButton("редактировать фото", callback_data="edit"))
    bot.reply_to(message, "прикольное фото", reply_markup=markup)

@bot.callback_query_handler(func=lambda callback: True)
def callback_message(callback):
    if callback.data == "delete":
        bot.delete_message(callback.message.chat.id, callback.message.message_id - 1)
    elif callback.data == "edit":
         bot.edit_message_text("Edit text", callback.message.chat.id, callback.message.message_id - 1)




bot.polling(none_stop=True )

