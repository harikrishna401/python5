# python5import random

class Player:
    def __init__(self, name):
        self.name = name
        self.health = 100
        self.attack_power = 10
        self.defense_power = 5

class Enemy:
    def __init__(self, name):
        self.name = name
        self.health = random.randint(50, 100)
        self.attack_power = random.randint(5, 15)

def battle(player, enemy):
    print(f"A wild {enemy.name} has appeared!\n")

    while player.health > 0 and enemy.health > 0:
        print(f"{player.name}'s Health: {player.health}")
        print(f"{enemy.name}'s Health: {enemy.health}\n")

        action = input("What will you do? (fight/flee): ")

        if action.lower() == "fight":
            enemy.health -= player.attack_power
            if enemy.health > 0:
                player.health -= max(0, enemy.attack_power - player.defense_power)
                print(f"You attacked {enemy.name} and dealt {player.attack_power} damage.")
                print(f"{enemy.name} attacked you and dealt {max(0, enemy.attack_power - player.defense_power)} damage.\n")
            else:
                print(f"You defeated {enemy.name}!\n")
        elif action.lower() == "flee":
            print("You managed to escape!\n")
            break
        else:
            print("Invalid choice. Try again.\n")

    if player.health <= 0:
        print("Game Over. You lose!")
    elif enemy.health <= 0:
        print("Congratulations! You defeated the enemy.")

def text_rpg():
    print("Welcome to the Text-based RPG!")

    player_name = input("Enter your name: ")
    player = Player(player_name)

    enemies = [Enemy("Goblin"), Enemy("Dragon"), Enemy("Orc"), Enemy("Skeleton")]

    while True:
        enemy = random.choice(enemies)
        battle(player, enemy)

        choice = input("Do you want to play again? (yes/no): ")
        if choice.lower() != 'yes':
            break

text_rpg()


import requests
from bs4 import BeautifulSoup

def simple_web_scraper(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')

    # Example: Scraping all headlines from a news website
    headlines = soup.find_all('h2', class_='headline')

    for headline in headlines:
        print(headline.text.strip())

# Example usage:
url = 'https://example.com/news'
simple_web_scraper(url)


from PIL import Image

def grayscale_image(input_image_path, output_image_path):
    try:
        original_image = Image.open(input_image_path)
        grayscale_image = original_image.convert("L")
        grayscale_image.save(output_image_path)
        grayscale_image.show()
        print("Grayscale image saved successfully.")

    except FileNotFoundError:
        print(f"Error: File '{input_image_path}' not found.")

# Example usage:
input_image_path = 'input_image.jpg'
output_image_path = 'grayscale_output.jpg'
grayscale_image(input_image_path, output_image_path)
