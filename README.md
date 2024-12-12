# Multi-Currency-Exchange-Hub-Accurate-Quick-Reliable
import customtkinter as ctk

# Define the color palette
BACKGROUND_COLOR = "#EDE7F6"
TEXT_COLOR = "#4A148C"
SECONDARY_TEXT_COLOR = "#7E57C2"
BUTTON_BACKGROUND_COLOR = "#8E24AA"
BUTTON_TEXT_COLOR = "#FFFFFF"
INPUT_BACKGROUND_COLOR = "#D1C4E9"
INPUT_TEXT_COLOR = "#311B92"

# Define the exchange rates dictionary
exchange_rates = {
    'USD': 1.0,
    'EUR': 1.05,
    'JPY': 110.53,
    'GBP': 0.75,
    'AUD': 1.35,
    'CAD': 1.25,
    'CHF': 0.92,
    'CNY': 6.45,
    'INR': 74.5,
    'BRL': 5.2,
    'ZAR': 14.7,
    'RUB': 74.0,
    'SGD': 1.34,
    'NZD': 1.44,
    'MXN': 20.2,
    'SEK': 8.7,
    'NOK': 8.4,
    'DKK': 6.3,
    'THB': 32.8,
    'MYR': 4.17,
    'KRW': 1170.0,
    'IDR': 14445.0,
    'PHP': 50.3,
    'PLN': 3.88,
    'TRY': 8.5,
    'HUF': 300.0,
    'CZK': 21.8,
    'ILS': 3.25,
    'CLP': 758.0,
    'EGP': 15.7,
    'AED': 3.67,
    'SAR': 3.75,
    'NGN': 410.0,
    'GEL':0.37,
}

# Function to perform currency conversion
def currency_converter(amount, from_currency, to_currency, exchange_rates):
    if from_currency in exchange_rates and to_currency in exchange_rates:
        if from_currency == to_currency:
            return amount
        base_amount = amount / exchange_rates[from_currency]
        converted_amount = base_amount * exchange_rates[to_currency]
        return converted_amount
    else:
        return "Conversion not possible with given currencies."

# Initialize the main window
app = ctk.CTk()
app.title("Currency Converter")
app.geometry("500x400")
app.configure(bg=BACKGROUND_COLOR)

# Create a label for title
title_label = ctk.CTkLabel(
    app,
    text="Currency Converter",
    text_color=TEXT_COLOR,
    font=("Helvetica", 24),
    bg_color=BACKGROUND_COLOR,
)
title_label.pack(pady=20)

# Create an entry for amount
amount_label = ctk.CTkLabel(
    app,
    text="Enter Amount:",
    text_color=SECONDARY_TEXT_COLOR,
    bg_color=BACKGROUND_COLOR,
)
amount_label.pack(pady=5)

amount_entry = ctk.CTkEntry(
    app,
    bg_color=INPUT_BACKGROUND_COLOR,
    text_color=INPUT_TEXT_COLOR,
    border_color=TEXT_COLOR,
)
amount_entry.pack(pady=5)

# Create dropdowns for currencies
from_currency_label = ctk.CTkLabel(
    app,
    text="From Currency:",
    text_color=SECONDARY_TEXT_COLOR,
    bg_color=BACKGROUND_COLOR,
)
from_currency_label.pack(pady=5)

from_currency_option = ctk.CTkOptionMenu(
    app, values=list(exchange_rates.keys()), fg_color=INPUT_BACKGROUND_COLOR
)
from_currency_option.pack(pady=5)

to_currency_label = ctk.CTkLabel(
    app,
    text="To Currency:",
    text_color=SECONDARY_TEXT_COLOR,
    bg_color=BACKGROUND_COLOR,
)
to_currency_label.pack(pady=5)

to_currency_option = ctk.CTkOptionMenu(
    app, values=list(exchange_rates.keys()), fg_color=INPUT_BACKGROUND_COLOR
)
to_currency_option.pack(pady=5)

# Function to handle button click and display result
def convert_currency():
    try:
        amount = float(amount_entry.get())
        from_currency = from_currency_option.get()
        to_currency = to_currency_option.get()
        converted_amount = currency_converter(amount, from_currency, to_currency, exchange_rates)
        if isinstance(converted_amount, float):
            result_label.configure(text=f"{amount} {from_currency} = {converted_amount:.2f} {to_currency}")
        else:
            result_label.configure(text=converted_amount)
    except ValueError:
        result_label.configure(text="Please enter a valid amount.")

# Create a button to trigger conversion
convert_button = ctk.CTkButton(
    app,
    text="Convert",
    command=convert_currency,
    fg_color=BUTTON_BACKGROUND_COLOR,
    text_color=BUTTON_TEXT_COLOR,
)
convert_button.pack(pady=20)

# Create a label to display the result
result_label = ctk.CTkLabel(
    app,
    text="",  
    text_color='#4A148C',
    bg_color='#FFFDD0',
    font=("Helvetica", 18)
)
result_label.pack(pady=20)

# Start the main loop
app.mainloop()
