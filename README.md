import phonenumbers
from phonenumbers import geocoder, carrier
import requests


def basic_osint(phone):
    try:
        p = phonenumbers.parse(phone)
        print("\n📌 BASIC OSINT")
        print("Davlat:", geocoder.description_for_number(p, "en"))
        print("Operator:", carrier.name_for_number(p, "en"))
        print("Valid:", phonenumbers.is_valid_number(p))
    except:
        print("❌ Raqam xato")


def google_osint(phone):
    print("\n🔍 GOOGLE OSINT")
    q = phone.replace("+", "")
    url = f"https://www.google.com/search?q={q}"
    r = requests.get(url, headers={"User-Agent": "Mozilla/5.0"})
    if "did not match any documents" in r.text:
        print("❌ Google’da topilmadi")
    else:
        print("✅ Google izlari bor")
        print(url)


phone = input("📞 Telefon raqamni kiriting (+998...): ")
basic_osint(phone)
google_osint(phone)
