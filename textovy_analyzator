# Definice platných uživatelských jmen a hesel
REGISTERED_USERS = {
    "bob": "123",
    "ann": "pass123",
    "mike": "password123",
    "liz": "pass123"
}

# 📄 Texty pro analýzu
TEXTS = [
    '''Situated about 10 miles west of Kemmerer,
    Fossil Butte is a ruggedly impressive
    topographic feature that rises sharply
    some 1000 feet above Twin Creek Valley
    to an elevation of more than 7500 feet
    above sea level. The butte is located just
    north of US 30 and the Union Pacific Railroad,
    which traverse the valley.''',
    '''At the base of Fossil Butte are the bright
    red, purple, yellow and gray beds of the Wasatch
    Formation. Eroded portions of these horizontal
    beds slope gradually upward from the valley floor
    and steepen abruptly. Overlying them and extending
    to the top of the butte are the much steeper
    buff-to-white beds of the Green River Formation,
    which are about 300 feet thick.''',
    '''The monument contains 8198 acres and protects
    a portion of the largest deposit of freshwater fish
    fossils in the world. The richest fossil fish deposits
    are found in multiple limestone layers, which lie some
    100 feet below the top of the butte. The fossils
    represent several varieties of perch, as well as
    other freshwater genera and herring similar to those
    in modern oceans. Other fish such as paddlefish,
    garpike and stingray are also present.'''
]

# 2. FUNKCE PRO VSTUP A OVĚŘENÍ

def get_user_input():
    """Zpracuje přihlášení a výběr textu. Vrátí vybraný text nebo None při selhání."""

    # --- Přihlášení uživatele ---
    print("Vítejte v programu pro analýzu textu.")
    username = input("Zadejte uživatelské jméno: ")
    password = input("Zadejte heslo: ")

    # ⚠️ Kontrola registrace: Pokud není platná dvojice, vrací None
    if username not in REGISTERED_USERS or REGISTERED_USERS[username] != password:
        print("Neplatné uživatelské jméno nebo heslo. Program bude ukončen.")
        return None

    print(f"\nVítej, {username}! Můžeš analyzovat texty.")

    # --- Výběr textu ---
    print("-" * 30)
    print("Máme k dispozici následující texty:")
    for i, text in enumerate(TEXTS):
        print(f"[{i + 1}] Text s délkou {len(text)} znaků.")

    try:
        selection_input = input(f"Vyber text (zadej číslo 1 - {len(TEXTS)}): ")

        selection_number = int(selection_input)

        # Kontrola, zda je číslo v platném rozsahu
        if 1 <= selection_number <= len(TEXTS):
            return TEXTS[selection_number - 1]
        else:
            print(f"Neplatné číslo textu (mimo rozsah 1 - {len(TEXTS)}). Program bude ukončen.")
            return None

    except ValueError:
        # Zachytí případ, kdy vstup není číslo
        print("Neplatný vstup. Je vyžadováno číslo. Program bude ukončen.")
        return None

# 3. FUNKCE PRO ANALÝZU A VÝSTUP

def analyze_text(text):
    """Provede veškerou textovou analýzu a zobrazí výsledky."""

    # Normalizace: nahradíme interpunkci mezerami
    normalized_text = re.sub(r'[.,:;!?"\'()]', ' ', text)

    # Rozdělení na "slova" (tokeny oddělené mezerami), zbavíme se prázdných řetězců
    words = [w for w in normalized_text.split() if w]

    # Inicializace počítadel
    count_all_words = len(words)
    count_title_case = 0
    count_upper_case = 0
    count_lower_case = 0
    count_numbers = 0
    sum_numbers = 0
    word_length_frequency = defaultdict(int)

    # Hlavní cyklus pro analýzu
    for word in words:

        if word.isdigit():
            # Čísla
            count_numbers += 1
            sum_numbers += int(word)
        else:
            # Slova
            if word.isupper():
                count_upper_case += 1
            elif word.islower():
                count_lower_case += 1
            elif word[0].isupper() and not word.isupper():
                count_title_case += 1

            # Četnost délek slov
            word_length_frequency[len(word)] += 1

    # --- Zobrazení výsledků ---
    print("-" * 30)
    print("VÝSLEDKY ANALÝZY:")
    print("-" * 30)
    print(f"Počet slov celkem (řetězec znaků oddělený mezerami): {count_all_words}")
    print(f"Počet slov začínajících velkým písmenem: {count_title_case}")
    print(f"Počet slov psaných VELKÝMI písmeny: {count_upper_case}")
    print(f"Počet slov psaných malými písmeny: {count_lower_case}")
    print(f"Počet čísel (tokenů): {count_numbers}")
    print(f"Součet všech čísel: {sum_numbers}")
    print("-" * 30)

    # Zobrazení sloupcového grafu
    print("GRAF ČETNOSTI DÉLEK SLOV:")
    for length in sorted(word_length_frequency.keys()):
        count = word_length_frequency[length]
        print(f"{length:2}: {'#' * count} ({count}x)")
    print("-" * 30)

# 4. HLAVNÍ SPOUŠTĚCÍ BLOK

def main():
    """Hlavní funkce programu."""
    selected_text = get_user_input()

    # Logika pro ukončení: Pokud selected_text je None, ukončíme program.
    if selected_text is None:
        return # Zajišťuje spolehlivé ukončení

    # Pokračuje analýza, pouze pokud byl text úspěšně vybrán.
    analyze_text(selected_text)

if __name__ == "__main__":
    main()
