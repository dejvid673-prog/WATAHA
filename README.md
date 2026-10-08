# WATAHA — agenci domenowi 7DEJV

## Cel
Repozytorium lokalnych definicji agentów związanych z operacjami commerce. Nie jest kanonicznym rejestrem współdzielonych agentów 7DEJV — ten znajduje się w [7dejv-agent-os](https://github.com/dejvid673-prog/7dejv-agent-os).

## Co znajduje się w repo
- [PrestaShop Commerce Agent](agents/prestashop-commerce-agent/AGENT.md) — zakres obowiązków, procedura audytu i ograniczenia dostępu;
- [Knowledge Sources](agents/prestashop-commerce-agent/KNOWLEDGE_SOURCES.md) — źródła wiedzy;
- `agents/prestashop-commerce-agent/.env.example` — wzór konfiguracji bez rzeczywistych poświadczeń.

## Status i granice
Agent ma w definicji profil **READ_ONLY** dla PrestaShop Webservice API. Obecność instrukcji nie potwierdza połączenia z działającym sklepem, instalacji ani przeprowadzenia testu end-to-end. Żadna operacja zapisu nie jest autoryzowana przez ten opis.

## Zasady pracy
1. Przeczytaj `AGENT.md` i `KNOWLEDGE_SOURCES.md` przed użyciem agenta.
2. Korzystaj z [repozytorium PrestaShop](https://github.com/dejvid673-prog/7dejv-prestashop) jako źródła prawdy dla kodu sklepu.
3. Nie zapisuj kluczy API, danych klientów ani plików `.env` w GitHub.
4. Rejestruj wyniki testów i ich ograniczenia, zanim oznaczysz integrację jako gotową.

Wszelkie zmiany uprawnień wymagają osobnej decyzji i weryfikacji.
