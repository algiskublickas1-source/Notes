import json

# ===============================
# Įkelti užrašus iš failo
# ===============================
def ikelti_uzrasus():
    global uzrasai
    try:
        with open("notes.json", "r") as f:
            uzrasai = json.load(f)
    except:
        uzrasai = []


# ===============================
# Išsaugoti užrašus į failą
# ===============================
def issaugoti_uzrasus():
    with open("notes.json", "w") as f:
        json.dump(uzrasai, f, indent=4)


# ===============================
# Pridėti užrašą
# ===============================
def prideti_uzrasa():
    pavadinimas = input("Įveskite užrašo pavadinimą: ")
    tekstas = input("Įveskite užrašo tekstą: ")

    uzrasas = {
        "pavadinimas": pavadinimas,
        "tekstas": tekstas
    }

    uzrasai.append(uzrasas)
    print("Užrašas pridėtas!")


# ===============================
# Rodyti visus užrašus
# ===============================
def rodyti_uzrasus():
    if len(uzrasai) == 0:
        print("Užrašų nėra.")
    else:
        print("\n--- Visi užrašai ---")
        for i, u in enumerate(uzrasai, start=1):
            print(f"{i}. {u['pavadinimas']} - {u['tekstas']}")


# ===============================
# Ištrinti užrašą pagal numerį
# ===============================
def istrinti_uzrasa():
    rodyti_uzrasus()

    try:
        nr = int(input("Įveskite užrašo numerį, kurį norite ištrinti: "))
        uzrasai.pop(nr - 1)
        print("Užrašas ištrintas!")
    except:
        print("Neteisingas numeris.")


# ===============================
# Redaguoti užrašą
# ===============================
def redaguoti_uzrasa():
    rodyti_uzrasus()

    try:
        nr = int(input("Įveskite užrašo numerį, kurį norite redaguoti: "))
        uzrasai[nr - 1]["pavadinimas"] = input("Naujas pavadinimas: ")
        uzrasai[nr - 1]["tekstas"] = input("Naujas tekstas: ")
        print("Užrašas atnaujintas!")
    except:
        print("Klaida: neteisingas numeris.")


# ===============================
# Meniu
# ===============================
ikelti_uzrasus()

while True:
    print("\n=== UŽRAŠŲ VALDYMO SISTEMA ===")
    print("1 - Pridėti užrašą")
    print("2 - Rodyti užrašus")
    print("3 - Ištrinti užrašą")
    print("4 - Redaguoti užrašą")
    print("5 - Išeiti")

    pasirinkimas = input("Pasirinkite: ")

    if pasirinkimas == "1":
        prideti_uzrasa()
    elif pasirinkimas == "2":
        rodyti_uzrasus()
    elif pasirinkimas == "3":
        istrinti_uzrasa()
    elif pasirinkimas == "4":
        redaguoti_uzrasa()
    elif pasirinkimas == "5":
        issaugoti_uzrasus()
        print("Užrašai išsaugoti. Viso gero!")
        break
    else:
        print("Neteisingas pasirinkimas!")
