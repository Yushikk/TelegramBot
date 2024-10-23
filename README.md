# TelegramBot
TelegramBot Ежедневник
from aiogram import Bot, Dispatcher
from aiogram.filters.command import Command
from aiogram.utils.keyboard import ReplyKeyboardBuilder, ReplyKeyboardMarkup, KeyboardButton
from aiogram.types import KeyboardButtonPollType



dp = Dispatcher()
bot = Bot(TOKEN)

@dp.message(Command('hello_name'))
async def command_hello_name(message):
  await message.answer('Привет, ' +  message.from_user.full_name)
@dp.message(Command('start'))
async def command_start(message):
  await message.answer('Привет, я твой бот-ежедневник! Выбери функцию чтобы начать:')
@dp.message(Command('help'))
async def command_help(message):
  await message.answer("""Всегда рад тебе помочь! Вот список команд, которые я могу выполнить
    /start - приветствие
    /help - расскажу о том, что умею
    /spec_kb - тут можно воспользоваться специальной клавиатурой
    /add - позволит добавлять дело в бот. Сначала он попросит вас ввести название самого дела, а затем выбрать день, когда нужно сделать.
    /show - покажет все добавленные дела в неделю.
    /delete - удалит конкретное дело из списка на конкретный день""")
def test_kb(user_telegram_id: int) -> ReplyKeyboardMarkup:
    kb_list = [
        [KeyboardButton(text="О нас"), KeyboardButton(text="Профиль")],
        [KeyboardButton(text="Заполнить анкету")],
        [KeyboardButton(text=" Уже есть аккаунт")],
    ]
    keyboard = ReplyKeyboardMarkup(keyboard=kb_list, resize_keyboard=True, one_time_keyboard=True)
    return keyboard

@dp.message(Command('spec_kb'))
async def specc_kb(message):
  await message.answer('Ты можешь воспользоваться специальной функцией', reply_markup=test_kb(message.from_user.id))



await dp.start_polling(bot)
