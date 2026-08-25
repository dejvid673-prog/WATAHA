# Knowledge Sources — PrestaShop Commerce Agent

Agent ma wiedzieć szerzej niż wynika z jego bieżących uprawnień wykonawczych. Wiedza i możliwość wykonania operacji są rozdzielone.

## 1. PrestaShop — obowiązkowa baza wiedzy

Przed zadaniem dotyczącym architektury, modułów, API, produktów lub diagnostyki korzystaj z istniejących skills w repozytorium `dejvid673-prog/7dejv-prestashop-resources`:

- `.ai/skills/prestashop-development-foundations`
- `.ai/skills/prestashop-internals-foundations`
- `.ai/skills/prestashop-product-browser-audit`
- `.ai/skills/prestashop-solution-architect`

Repozytorium wiedzy PrestaShop jest źródłem referencyjnym. Nie kopiuj całej wiedzy do WATAHA i nie twórz jej duplikatu. Czytaj aktualną wersję źródła przed zadaniem, jeśli jest dostępna.

Domyślny target projektu: PrestaShop 9, chyba że realny sklep/repozytorium wskazuje inaczej.

Zasady: nie modyfikuj core; preferuj moduły, hooki, usługi Symfony, API, oddzielne tabele i minimalny zakres zmian. Faktyczny kod sklepu, modułu i odpowiedź API mają pierwszeństwo przed wiedzą ogólną.

## 2. Produkty STAW EXPERT i produkty wędkarskie

Dla wiedzy produktowej korzystaj z `dejvid673-prog/7dejv-staw-expert`, szczególnie:

- `00_START_HERE.md`
- `00_GLOBAL_RULES_STAW_EXPERT.md`
- `00_REPO_INDEX.md`
- `02_produkty/`
- `05_opisy_seo/`
- `07_regulacje-i-bezpieczenstwo/`
- `08_product-os/`
- `08_sprzedaz-i-kanaly/`
- `09_ceny-logistyka/`

Agent ma rozpoznawać przynajmniej klasy produktów istotne operacyjnie: zanęty, kulki proteinowe/zanętowe/przynętowe, pellety, dodatki i atraktory, minerały/kreda, preparaty do stawów/wody, opakowania oraz produkty wykluczone z określonych marketplace według polityk systemowych.

Nie utożsamiaj nazwy handlowej z funkcją produktu. Np. pellet lub kulka może być zanętowa albo przynętowa; klasyfikację opieraj na danych produktu i zatwierdzonych regułach.

Nie wymyślaj składu, działania, zastosowania, bezpieczeństwa, EAN, masy, parametrów ani deklaracji marketingowych.

## 3. Opakowania i logistyka

Źródłem zasad jest m.in. `dejvid673-prog/7dejv-staw-expert/09_ceny-logistyka/szablon-logistyki-opakowania.md`.

Agent ma rozróżniać:

- masę netto produktu,
- masę brutto produktu w opakowaniu jednostkowym,
- masę brutto gotowej przesyłki,
- opakowanie jednostkowe,
- opakowanie wysyłkowe,
- wypełnienie/zabezpieczenie,
- wymiary produktu,
- finalne wymiary paczki,
- liczbę sztuk w paczce,
- ograniczenia przewoźnika/kanału,
- ryzyko uszkodzenia, wilgoci, wycieku, zgniecenia etykiety i przekroczenia masy/gabarytu.

Typowe opakowania domenowe, które agent powinien rozpoznawać: kanister/bańka, wiadro, słoik, worek, saszetka/doypack, karton, koperta. Konkretne parametry zawsze muszą pochodzić z danych źródłowych.

Przy wielopakach nie mnożysz bezmyślnie stanu. Dostępność wielopaku zależy od stanu SKU bazowego, liczby sztuk, masy i ograniczeń logistycznych. Wielopaki są etapem późniejszym, dopóki polityka nie zostanie zatwierdzona.

## 4. Nadawanie paczek — wiedza vs wykonanie

Agent ma znać proces przesyłki i umieć go audytować:

`zamówienie -> walidacja danych -> wybór usługi -> parametry paczki -> utworzenie przesyłki -> etykieta -> tracking -> status -> audyt powykonawczy`.

Powinien rozumieć integracje przewoźników i modułów sklepu na podstawie repozytorium oraz faktycznie dostępnych API. Nie zakładaj, że dana metoda nadania istnieje bez sprawdzenia dokumentacji/API/modułu.

### Aktualna blokada wykonawcza

Bieżący klucz PrestaShop Webservice jest GET-only. Agent NIE MOŻE obecnie nadawać paczek ani zmieniać zamówień w PrestaShop.

Może:

- czytać zamówienia i dane logistyczne dostępne przez GET,
- sprawdzać gotowość do nadania,
- przygotowywać plan nadania,
- audytować przesyłki, jeśli identyfikatory/statusy są dostępne do odczytu,
- wykrywać brak etykiety/tracking/statusu na podstawie dostępnych dowodów.

Faktyczne nadawanie będzie dozwolone dopiero po wdrożeniu osobnego connectora z minimalnymi uprawnieniami zapisu i zatwierdzeniu jego polityki.

## 5. Obowiązkowy audyt po operacji

Dla każdej przyszłej operacji wykonawczej, w tym publikacji produktu lub nadania paczki:

1. zapisz planowaną liczbę obiektów,
2. wykonaj operację,
3. ponownie odczytaj stan z systemu źródłowego,
4. porównaj plan z rzeczywistością,
5. sprawdź identyfikatory, statusy i artefakty (np. tracking/etykieta),
6. zakończ `VERIFIED_COMPLETE`, `PARTIAL` albo `FAILED`.

Samo HTTP 2xx, komunikat UI lub deklaracja innego agenta nie jest dowodem wykonania.

## 6. Hierarchia źródeł

1. realna odpowiedź API / stan sklepu,
2. repozytorium projektu i jego aktualna dokumentacja,
3. oficjalna dokumentacja producenta/platformy,
4. zatwierdzone polityki WATAHA/7DEJV,
5. wiedza ogólna modelu.

Przy konflikcie zgłoś konflikt zamiast arbitralnie wybierać wygodniejszą wersję.
