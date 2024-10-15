import openai
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters

# Укажи свои токены Telegram и OpenAI
TELEGRAM_TOKEN = "7735911622:AAFOI1P7dR4uRKIL1A_04SBR0kp7hND89us"
OPENAI_API_KEY = ("sk-proj-5F6adfwOBm64jAZMRJqIi8rmYByjfsmhad"
                  "vJicMMouGJ6Q-OsCMLTI74mGkORFm8xCoQp-VlpoT3BlbkFJ3uEnCs0vZYBWiK"
                  "OZOTFH_ADItTx_6grD0LxJrj2DZWm6XmmSPBR9ar2UFU1RQkfQvRFH887e8A")

# Установи API-ключ OpenAI
openai.api_key = OPENAI_API_KEY

# Функция для получения ответа от OpenAI через новый интерфейс
def get_ai_response(user_message):
    try:
        # Используем новый интерфейс для генерации ответа
        response = openai.completions.create(
            model="gpt-4",  # Или gpt-3.5-turbo, если доступно
            prompt=user_message,
            max_tokens=150,
            temperature=0.7
        )
        return response['choices'][0]['text'].strip()

    except Exception as e:
        return f"Ошибка при обращении к OpenAI API: {e}"

# Команда /start для приветствия
async def start(update: Update, context):
    await update.message.reply_text("Привет! Я бот, задавай свои вопросы.")

# Обработка текстовых сообщений
async def handle_message(update: Update, context):
    user_message = update.message.text
    # Получаем ответ от AI
    ai_response = get_ai_response(user_message)
    await update.message.reply_text(ai_response)

# Основной код запуска бота
if __name__ == '__main__':
    # Создаем приложение Telegram
    application = ApplicationBuilder().token(TELEGRAM_TOKEN).build()

    # Добавляем обработчики команд и сообщений
    application.add_handler(CommandHandler('start', start))
    application.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

    # Запуск бота
    application.run_polling()
