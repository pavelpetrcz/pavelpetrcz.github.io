## **Podpis RSA klíčem v Jupyter Lab krok za krokem**

Pro jeden z pracovních úkolů bylo nezbytné rozchodit podepisování a ověřování sadou klíčů. Aby vývoj probíhal hladce a bez zbytečných zádrhelů tak z mého subjektivního pohledu je nejlepší, když vývojářům dáte jasné zadání k jaké hodnotě se mají dopočíst.

Rozhodnutí sestavit referenční způsob výpočtu s hodnotami mezivýsledků jsem učinil i s vědomím, že kolegové vývojáři budou reálné výpočty dělat ve třech jazycích jako Swift, Kotlin a Java.

V neposlední řadě byla jednodušší komunikace s kolegy z týmu zabývající se zabezpečením. Validace probíhala na hmatatelných výsledcích místo slovního zadání, které může zejména v oblasti kryptografie trpět v důsledku řady možných parametrů - od zvolených šifer, jejich verzí, přes vybraná schémata, standardy, etc.

##### **Samotný výpočet**

Za předpokladu, že máte instalovanou Anacondu tak v hlavní nabídce Windows vyhledejte její příkazovou řádku - Anaconda Prompt a tu spusťte. Nyní příkazem spusťte Jupyter Lab.

`jupyter lab`

V něm vytvořte nový notebook ve kterém celou referenční implementaci provedeme. Pro jednoduchost jsem připravil Gist na Githubu, kde si můžete celý postup stáhnout a importovat.

{% gist 58bca38328536d2b86d71af6cdf9a6db %}

Princip výpočtu je jednoduchý a v Gistu popsaný, ale i tak ho stručně popíši ještě sem s nějakými vedlejšími poznámkami pokud budou potřeba.

* V úvodní části importujeme potřebné knihovny - pozor nespleťte si **Cryptodome** a **Crypto**. Pokud budete mít nainstalované obě dvě, pak se dočkáte jen samých problémů. Python nebude vědět se kterou chcete pracovat. Obě knihovny mají metody pojmenované stejně - Crypto je předchůdce Cryptodome, tím to je. Proto na to upozorňuji. Sám jsem se s tím potýkal a velmi vřele doporučuji pracovat s Cryptodome. Instalace vás nemine pokud jste si Anacondu nainstalovali právě teď.
* Následuje načtení základní proměnných - zprávy, co se bude podepisovat, a dvou klíčů - veřejného a privátního.
* Následuje výpočet samotného podpisu zprávy privátním klíčem ve vybraném schématu.
* Následně se vypočtený hash převádí do podoby HEX a Base64. Cílem zveřejnění daných mezivýpočtů je právě verifikovatelnost správnosti implementace v libovolném jazyce (prostě jestli mi to leze z konzole IDE, to co vidím v zadání).
* Na konci je pouze kus kodu, který potvrzuje správnost výpočtu opačným postupem. Tedy ověřením, že podpis zprávy je validní.

Na začátku jsem si nebyl zcela jistý tím, že někdo mou ukázku, jak to vypočítat, ocení. Se svou ukázkou v Pythonu jsem vlastně pořídil dost muziky. Soubor jsem k zadání přikládal jen jakoby navíc, ale nakonec se stal primárním zdrojem inspirace pro faktickou implementaci.

##### **Závěr**

* najděte si způsob, jak tu nejtěžší část vývojového úkolu vizualizovat, nakreslit nebo nabouchat, abyste si všichni rozuměli a odladili nejasnosti
* dost řešení chyb začíná "já myslel, že myslíš, abych" - takto zavání nepřesné nebo neúplné zadání; vyhněte se tomu obloukem, když to jde
* a nakonec je to taky legranda se něco přiučit nového

##### **Zdroje**

* [https://www.pycryptodome.org/en/latest/src/signature/pkcs1_v1_5.html?highlight=sign#pkcs-1-v1-5-rsa](https://www.pycryptodome.org/en/latest/src/signature/pkcs1_v1_5.html?highlight=sign#pkcs-1-v1-5-rsa)
* [https://tools.ietf.org/html/rfc8017](https://tools.ietf.org/html/rfc8017)
