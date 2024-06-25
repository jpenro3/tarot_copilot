"""
Tarot Card Reading Simulation

This script simulates a tarot card reading session with various predefined layouts (spreads) using 
a full tarot deck. The deck consists of both Major Arcana and Minor Arcana cards. The primary features 
of this script include:

1. TarotSession Class:
   - Manages the deck of tarot cards.
   - Supports drawing cards from the deck, ensuring no duplicates within a session.
   - Resets the deck for a new session.

2. Card Meanings:
   - Provides interpretations for each card in both upright and reversed orientations.
   - Card meanings are stored in an external JSON file (`card_meanings.json`).

3. Layouts (Spreads):
   - Predefined tarot spreads such as three-card, Celtic Cross, one-card, and many more.
   - Each layout has specific positions with meanings.
   - Spread layouts are stored in an external JSON file (`spread_layouts.json`).

4. Numerology, Color Theory, and Hidden Meanings:
   - Provides additional layers of interpretation for each card.
   - Data for numerology, color theory, and hidden meanings are stored in external JSON files 
     (`numerology.json`, `color_theory.json`, and `hidden_meanings.json` respectively).

5. Reading Creation:
   - Generates a tarot reading based on drawn cards and the chosen layout.
   - Each card is explained with its position meaning, interpretation, hidden symbols, numerology, 
     and color theory.

6. User Interaction:
   - Prompts the user to choose a layout and optionally provide a question or focus for the reading.
   - Displays the generated reading with detailed explanations for each card and its position.

Security and Randomness:
   - Utilizes the 'secrets' module to ensure cryptographically secure random selections for card draws and orientations.

Example Usage:
   - The user is prompted to select a tarot layout and optionally provide a focus for the reading.
   - The script then draws the appropriate number of cards, interprets them, and prints a detailed reading.

This script is designed to provide an engaging and insightful tarot reading experience by emphasizing the 
exploration of hidden symbols, numerology, and color theory within the cards.
"""

import secrets
import json

# Load JSON data
def load_json_file(file_path):
    with open(file_path, 'r') as file:
        return json.load(file)

# Load card meanings, spread layouts, numerology, color theory, and hidden meanings
tarot_card_meanings = load_json_file('card_meanings.json')
spread_layouts = load_json_file('spread_layouts.json')
numerology_data = load_json_file('numerology.json')
color_theory_data = load_json_file('color_theory.json')
hidden_meanings_data = load_json_file('hidden_meanings.json')

# Tarot Session Management
class TarotSession:
    def __init__(self):
        self.reset_deck()

    def reset_deck(self):
        self.deck = [
            "The Fool", "The Magician", "The High Priestess", "The Empress", "The Emperor",
            "The Hierophant", "The Lovers", "The Chariot", "Strength", "The Hermit",
            "Wheel of Fortune", "Justice", "The Hanged Man", "Death", "Temperance",
            "The Devil", "The Tower", "The Star", "The Moon", "The Sun",
            "Judgement", "The World", "Ace of Wands", "Two of Wands", "Three of Wands",
            "Four of Wands", "Five of Wands", "Six of Wands", "Seven of Wands", "Eight of Wands",
            "Nine of Wands", "Ten of Wands", "Page of Wands", "Knight of Wands", "Queen of Wands",
            "King of Wands", "Ace of Cups", "Two of Cups", "Three of Cups", "Four of Cups",
            "Five of Cups", "Six of Cups", "Seven of Cups", "Eight of Cups", "Nine of Cups",
            "Ten of Cups", "Page of Cups", "Knight of Cups", "Queen of Cups", "King of Cups",
            "Ace of Swords", "Two of Swords", "Three of Swords", "Four of Swords", "Five of Swords",
            "Six of Swords", "Seven of Swords", "Eight of Swords", "Nine of Swords", "Ten of Swords",
            "Page of Swords", "Knight of Swords", "Queen of Swords", "King of Swords",
            "Ace of Pentacles", "Two of Pentacles", "Three of Pentacles", "Four of Pentacles",
            "Five of Pentacles", "Six of Pentacles", "Seven of Pentacles", "Eight of Pentacles",
            "Nine of Pentacles", "Ten of Pentacles", "Page of Pentacles", "Knight of Pentacles",
            "Queen of Pentacles", "King of Pentacles"
        ]
        self.drawn_cards = []

    def draw_cards(self, number_of_cards):
        drawn_cards = []
        for _ in range(number_of_cards):
            if len(self.deck) == 0:
                print("No more cards to draw.")
                break  # No more cards to draw
            card = secrets.choice(self.deck)
            self.deck.remove(card)
            card_orientation = secrets.choice(["Upright", "Reversed"])
            drawn_cards.append((card, card_orientation))
            self.drawn_cards.append((card, card_orientation))
        return drawn_cards

# Interpretation Function
def interpret_card(card, orientation):
    meaning = tarot_card_meanings.get(card, {}).get(orientation, "No meaning found.")
    return meaning

# Create Reading with Positions
def create_reading(drawn_cards, layout_name):
    layout = spread_layouts.get(layout_name)
    if not layout:
        raise ValueError(f"Layout '{layout_name}' is not defined.")
    if len(drawn_cards) != len(layout['positions']):
        raise ValueError(f"{layout_name} layout requires exactly {len(layout['positions'])} cards.")

    reading = []
    for i, (card, orientation) in enumerate(drawn_cards):
        position_meaning = layout['positions'][i]
        meaning = interpret_card(card, orientation)
        hidden_symbols = hidden_meanings_data.get(card, "No hidden symbols found.")
        numerology = numerology_data.get(card, "No numerology found.")
        color_theory = color_theory_data.get(card, "No color theory found.")
        
        reading.append({
            "Position": position_meaning,
            "Card": card,
            "Orientation": orientation,
            "Meaning": meaning,
            "Hidden Symbols": hidden_symbols,
            "Numerology": numerology,
            "Color Theory": color_theory
        })
    return reading

# Prompt the user for input
def get_user_input():
    print("Available layouts:")
    for layout_name in spread_layouts.keys():
        print(f" - {layout_name}")

    layout_choice = input("Choose a layout: ").strip()
    question = input("Do you have a specific question or focus for this reading? (optional): ").strip()
    
    return layout_choice, question

# Example Usage
layout_choice, question = get_user_input()
session = TarotSession()
layout = spread_layouts.get(layout_choice)

if layout:
    drawn_cards = session.draw_cards(len(layout['positions']))
    reading = create_reading(drawn_cards, layout_choice)

    print(f"Reading for your question/focus: '{question}'" if question else "Reading:")

    for card_reading in reading:
        print(f"Position: {card_reading['Position']}")
        print(f"Card: {card_reading['Card']} ({card_reading['Orientation']})")
        print(f"Meaning: {card_reading['Meaning']}")
        print(f"Hidden Symbols: {card_reading['Hidden Symbols']}")
        print(f"Numerology: {card_reading['Numerology']}")
        print(f"Color Theory: {card_reading['Color Theory']}")
        print("----------")
else:
    print(f"Layout '{layout_choice}' is not defined.")
