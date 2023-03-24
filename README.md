<h1 class="title">1. Úloha IOS (2023)</h1>
                  <div class="row">
            <div class="col-xl-10"><h1 id="popis-úlohy">Popis úlohy</h1>
<p>Česká kontrarozvědka FDTO (<strong>F</strong>akt
<strong>D</strong>ěsně <strong>T</strong>ajná
<strong>O</strong>rganizace) má podezření, že v jejích řadách působí
krtek a služba tak byla kompromitována. Obsah některých přísně tajných
digitálních dokumentů byl nejenže vyzrazen tajným službám cizích
mocností, ale zřejmě i modifikován, což způsobilo chaos v organizaci
některých tajných operací a částečně tak paralyzovalo fungování celé
kontrarozvědky. V zájmu národní bezpečnosti je zapotřebí krtka urychleně
najít a polapit. Hledání však musí být maximálně diskrétní, aby krtek
netušil, že se okolo něj utahuje smyčka.</p>
<p>Protože zavedení nových oficiálních bezpečnostních opatření při práci
s utajovanými digitálními dokumenty by mohlo být podezřelé a krtka
vyplašit, rozhodlo se vedení kontrarozvědky, že bude potřeba tato
bezpečností opatření zavést utajeně. Tedy tak, aby si nikdo (kromě
nejužšího vedení a Vás) nebyl vědom toho, že nějaká nová opatření vešla
v platnost.</p>
<p>Vzhledem k Vaší léty prověřené loajalitě a bezchybné pracovní
historii v IT jednotce kontrarozvědky jste byli pro tuto tajnou misi
vybráni právě Vy. Vaším úkolem je vytvořit skript, který bude
prezentován jako nový interní nástroj pro zvýšení efektivity při práci s
elektronickými dokumenty, zatímco skrytě bude použit pro tajné
zaznamenávání (tzv. logging) a ohlašování informací o tom, se kterými
dokumenty (a kdy) daný uživatel pracoval.</p>
<p>Citlivé dokumenty jsou v kontrarozvědce zásadně uchovávány na
serverech a přístup k nim probíhá vzdáleně pomocí příslušných nástrojů.
Skript <code>mole</code> (<strong>M</strong>akes <strong>O</strong>ne’s
<strong>L</strong>ife <strong>E</strong>asier) tedy bude fungovat jako
tzv. wrapper nad textovými editory, což znamená, že textový editor bude
spouštěn skrze skript <code>mole</code>. Skript si bude pamatovat, které
soubory byly v jakém adresáři prostřednictvím skriptu <code>mole</code>
editovány. Jednotlivé soubory je zároveň možné přiřazovat do skupin pro
jednodušší filtrování při práci s velkým množstvím souborů. Pokud bude
skript spuštěn bez parametrů, vybere skript soubor, který má být
editován.</p>
<h1 id="specifikace-chování-skriptu">Specifikace chování skriptu</h1>
<p><strong>JMÉNO</strong></p>
<ul>
<li><code>mole</code> – wrapper pro efektivní použití textového editoru
s možností automatického výběru nejčastěji či posledně modifikovaného
souboru.</li>
</ul>
<p><strong>POUŽITÍ</strong></p>
<ul>
<li><code>mole -h</code></li>
<li><code>mole [-g GROUP] FILE</code></li>
<li><code>mole [-m] [FILTERS] [DIRECTORY]</code></li>
<li><code>mole list [FILTERS] [DIRECTORY]</code></li>
<li><code>mole secret-log [-b DATE] [-a DATE] [DIRECTORY1 [DIRECTORY2 [...]]]</code></li>
</ul>
<h1 id="popis">Popis</h1>
<ul>
<li><code>-h</code> – Vypíše nápovědu k použití skriptu (volba
<code>secret-log</code> by neměla být v nápovědě uvedena; nechceme krtka
upozornit, že sbíráme informace).</li>
<li><code>mole [-g GROUP] FILE</code> – Zadaný soubor bude otevřen.
<ul>
<li>Pokud byl zadán přepínač <code>-g</code>, dané otevření souboru bude
zároveň přiřazeno do skupiny s názvem <code>GROUP</code>.
<code>GROUP</code> může být název jak existující, tak nové skupiny.</li>
</ul></li>
<li><code>mole [-m] [FILTERS] [DIRECTORY]</code> – Pokud
<code>DIRECTORY</code> odpovídá existujícímu adresáři, skript z daného
adresáře vybere soubor, který má být otevřen.
<ul>
<li>Pokud nebyl zadán adresář, předpokládá se aktuální adresář.</li>
<li>Pokud bylo v daném adresáři editováno skriptem více souborů, vybere
se soubor, který byl pomocí skriptu otevřen (editován) jako
<strong>poslední</strong>.</li>
<li>Pokud byl zadán argument <code>-m</code>, tak skript vybere soubor,
který byl pomocí skriptu otevřen (editován) <strong>nejčastěji</strong>.
<ul>
<li>Pokud bude při použití přepínače <code>-m</code> nalezeno více
souborů se stejným maximálním počtem otevření, může <code>mole</code>
vybrat kterýkoliv z nich.</li>
</ul></li>
<li>Výběr souboru může být dále ovlivněn zadanými filtry
<code>FILTERS</code>.</li>
<li>Pokud nebyl v daném adresáři otevřen (editován) ještě žádný soubor,
případně žádný soubor nevyhovuje zadaným filtrům, jedná se o chybu.</li>
</ul></li>
<li><code>mole list [FILTERS] [DIRECTORY]</code> – Skript zobrazí seznam
souborů, které byly v daném adresáři otevřeny (editovány) pomocí
skriptu.
<ul>
<li>Pokud nebyl zadán adresář, předpokládá se aktuální adresář.</li>
<li>Seznam souborů může být filtrován pomocí <code>FILTERS</code>.</li>
<li>Seznam souborů bude lexikograficky seřazen a každý soubor bude
uveden na samostatném řádku.</li>
<li>Každý řádek bude mít formát
<code>FILENAME:&lt;INDENT&gt;GROUP_1,GROUP_2,...</code>, kde
<code>FILENAME</code> je jméno souboru (i s jeho případnými příponami),
<code>&lt;INDENT&gt;</code> je počet mezer potřebných k zarovnání a
<code>GROUP_*</code> jsou názvy skupin, u kterých je soubor evidován.
<ul>
<li>Seznam skupin bude lexikograficky seřazen.</li>
<li>Pokud budou skupiny upřesněny pomocí přepínače <code>-g</code> (viz
sekce FILTRY), uvažujte při výpisu souborů a skupin pouze záznamy
patřící do těchto skupin.</li>
<li>Pokud soubor nepatří do žádné skupiny, bude namísto seznamu skupin
vypsán pouze znak <code>-</code>.</li>
<li>Minimální počet mezer použitých k zarovnání (<code>INDENT</code>) je
jedna. Každý řádek bude zarovnán tak, aby seznam skupin začínal na
stejné pozici. Tedy např:</li>
</ul>
<pre><code>FILE1:  grp1,grp2
FILE10: grp1,grp3
FILE:   -</code></pre></li>
</ul></li>
<li><code>mole secret-log [-b DATE] [-a DATE] [DIRECTORY1 [DIRECTORY2 [...]]]</code>
– Skript za účelem dopadení krtka vytvoří tajný komprimovaný log s
informacemi o souborech otevřených (editovaných) skrze skript
<code>mole</code>.
<ul>
<li>Pokud byly zadány adresáře, tajný log bude obsahovat záznamy o
otevřených (editovaných) souborech pouze z těchto adresářů. Neexistující
adresáře nebo adresáře bez záznamů budou ignorovány.</li>
<li>Pokud nebyl zadán žádný adresář, tajný log bude obsahovat záznamy ze
všech evidovaných adresářů.</li>
<li>Otevřené (editované) soubory, které mají být v tajném logu
zaznamenány, je možné dále omezit pomocí filtrů <code>-a</code> a
<code>-b</code> (viz níže).</li>
</ul></li>
</ul>
<h1 id="filtry">Filtry</h1>
<p><code>FILTERS</code> může být kombinace následujících filtrů (každý
může být uveden maximálně jednou):</p>
<ul>
<li><code>[-g GROUP1[,GROUP2[,...]]]</code> – Specifikace skupin. Soubor
bude uvažován (pro potřeby otevření nebo výpisu) pouze tehdy, pokud jeho
spuštění spadá alespoň do jedné z těchto skupin.</li>
<li><code>[-a DATE]</code> - Záznamy o otevřených (editovaných)
souborech před tímto datem <strong>včetně (volitelně lze implementovat i
jako striktně před uvedeným datem; UPDATED 22.3.)</strong> nebudou
uvažovány.</li>
<li><code>[-b DATE]</code> - Záznamy o otevřených (editovaných)
souborech po tomto datu <strong>včetně (volitelně lze implementovat i
jako striktně po uvedeném datu; UPDATED 22.3.)</strong> nebudou
uvažovány.</li>
<li>Argument <code>DATE</code> je ve formátu
<code>YYYY-MM-DD</code>.</li>
</ul>
<h1 id="nastavení-a-konfigurace">Nastavení a konfigurace</h1>
<ul>
<li>Skript si pamatuje informace o svém spouštění v souboru, který je
dán proměnnou <code>MOLE_RC</code>. Formát souboru není specifikován.
<ul>
<li>Pokud není proměnná nastavena, jedná se o chybu.</li>
<li>Pokud soubor na cestě dané proměnnou <code>MOLE_RC</code>
neexistuje, soubor bude vytvořen včetně cesty k danému souboru (pokud i
ta neexistuje).</li>
</ul></li>
<li>Skript spouští editor, který je nastaven v proměnné
<code>EDITOR</code>. Pokud není proměnná <code>EDITOR</code> nastavená,
respektuje proměnnou <code>VISUAL</code>. Pokud ani ta není nastavená,
použije se příkaz <code>vi</code>.</li>
</ul>
<h1 id="formát-tajného-logu">Formát tajného logu</h1>
<ul>
<li>Tajný log vygenerovaný pomocí příkazu <code>secret-log</code> bude
uložen v adresáři <code>.mole</code> umístěném v domovském adresáři
(tedy např. <code>/home/$USER/.mole/</code>). Název souboru bude ve
formátu <code>log_USER_DATETIME.bz2</code>, kde <code>USER</code>
odpovídá jménu aktuálního uživatele a <code>DATETIME</code> odpovídá
datu a času vytvoření tajného logu.
<ul>
<li>Tajný log bude obsahovat záznamy o všech známých manipulacích (tedy
otevření skrze skript <code>mole</code>) s vybranými soubory, případně
dále omezených na daný časový úsek pomocí přepínačů <code>-a</code>,
<code>-b</code>, nebo jejich kombinací.</li>
<li>Formát záznamů v logu bude
<code>FILEPATH;DATETIME_1;DATETIME_2;...</code>, kde
<ul>
<li><code>FILEPATH</code> je reálná cesta k souboru,</li>
<li><code>DATETIME_N</code> je datum a čas chronologicky
<code>N</code>-tého známého otevření souboru buď napříč celou známou
historií, nebo v daném časovém úseku.</li>
</ul></li>
<li>Záznamy v tajném logu budou seřazeny lexikograficky podle hodnoty
<code>FILEPATH</code>.</li>
</ul></li>
<li>Formát hodnot <code>DATETIME</code> a <code>DATETIME_N</code> je
<code>YYYY-MM-DD_HH-mm-ss</code>.</li>
<li>Tajný log komprimujte pomocí utility <code>bzip2</code>.</li>
</ul>
<h1 id="poznámky">Poznámky</h1>
<ul>
<li>Můžete předpokládat, že nebude zadána skupina se jménem
<code>-</code> a že názvy skupin nebudou obsahovat znak čárky</li>
<li>Můžete předpokládat, že názvy souborů (ani jejich cesty) nebudou
obsahovat znaky středníku nebo dvojtečky.</li>
<li>Skript nebere v potaz otevření nebo editace, které byly provedeny
mimo skript <code>mole</code>.</li>
<li>Stejně tak pro příkaz <code>mole [-m] [FILTERS] [DIRECTORY]</code>
skript nebere v potaz soubory, se kterými dříve počítal a které jsou
nyní smazané (u ostatních příkazů není potřeba kontrolovat existenci
souboru). Například, pokud byl <em>posledně</em> editovaný soubor
smazán, volání <code>mole</code> otevře <em>předposledně</em> editovaný
soubor, pokud byl i ten smazán, bude otevřen <em>předpředposledně</em>
editovaný soubor, atp. <strong>UPDATED 6.3.</strong></li>
<li>Při rozhodování relativní cesty adresáře je doporučené používat
reálnou cestu (realpath). Důvod např.:</li>
</ul>
<div class="sourceCode" id="cb2"><pre class="sourceCode sh"><code class="sourceCode bash"><span id="cb2-1"><a href="file:///Users/ondra/teaching/ios/ios-23-1/zadani_reseni/README.html#cb2-1" aria-hidden="true" tabindex="-1"></a><span class="ex">$</span> mole .</span>
<span id="cb2-2"><a href="file:///Users/ondra/teaching/ios/ios-23-1/zadani_reseni/README.html#cb2-2" aria-hidden="true" tabindex="-1"></a><span class="ex">$</span> mole <span class="kw">`</span><span class="bu">pwd</span><span class="kw">`</span></span></code></pre></div>
<h1 id="návratová-hodnota">Návratová hodnota</h1>
<ul>
<li>Skript vrací úspěch v případě úspěšné operace nebo v případě úspěšné
editace. Pokud editor vrátí chybu, skript vrátí stejný chybový návratový
kód. Interní chyba skriptu bude doprovázena chybovým hlášením.</li>
</ul>
<h1 id="implementační-detaily">Implementační detaily</h1>
<ul>
<li>Skript by měl mít v celém běhu nastaveno
<code>POSIXLY_CORRECT=yes</code>.</li>
<li>Skript by měl běžet na všech běžných shellech (dash, ksh, bash).
Můžete použít GNU rozšíření pro <code>sed</code> či <code>awk</code>.
Jazyk Perl nebo Python povolen není.</li>
<li>Skript by měl ošetřit i chybový případ, že na daném stroji utilita
<code>realpath</code> není dostupná (např. ukončením programu s chybovým
kódem).</li>
<li><strong>UPOZORNĚNÍ:</strong> některé servery, např.
<code>merlin.fit.vutbr.cz</code>, mají symlink
<code>/bin/sh -&gt; bash</code>. Ověřte si proto, že skript skutečně
testujete daným shellem. Doporučujeme ověřit správnou funkčnost pomocí
virtuálního stroje níže.</li>
<li>Skript musí běžet na běžně dostupných OS GNU/Linux, BSD a MacOS.
Studentům je k dispozici virtuální stroj, na kterém lze ověřit správnou
funkčnost projektu, s obrazem ke stažení zde: <a href="http://www.fit.vutbr.cz/~lengal/public/trusty.ova">http://www.fit.vutbr.cz/~lengal/public/trusty.ova</a>
(pro VirtualBox, login: <code>trusty</code> / heslo:
<code>trusty</code>).</li>
<li>Skript nesmí používat dočasné soubory. Povoleny jsou však dočasné
soubory nepřímo tvořené jinými příkazy (např. příkazem
<code>sed -i</code>). Soubor <code>MOLE_RC</code> ani tajné log soubory
nejsou v tomto případě chápány jako dočasné soubory.</li>
<li>Není potřeba řešit možnost souběhu několika instancí skriptu, v
takovém případě je chování nedefinované.</li>
</ul>
<h1 id="možná-rozšíření">Možná rozšíření</h1>
<ul>
<li>Implementuje u příkazů <code>mole [-m] [FILTERS] [DIRECTORY]</code>,
<code>list</code> a <code>secret-log</code> nový přepínač
<code>-r</code> (recursive), který způsobí, že <code>mole</code> bude
hledat vyhovující záznamy o otevření (editaci) souborů i mezi záznamy,
které se vztahují ke vnořeným adresářům vzhledem k
<code>DIRECTORY</code> (resp. aktuálnímu adresáři, pokud nebyl
<code>DIRECTORY</code> zadán).
<ul>
<li>Tedy například příkaz <code>mole list ~/proj1</code> by na výstup
vypsal jak soubor <code>main.c</code>, tak soubor
<code>.git/config</code> za předpokladu, že má v logu
<code>MOLE_RC</code> uloženy záznamy o otevření souborů
<code>~/proj1/main.c</code> a <code>~/proj1/.git/config</code>.</li>
</ul></li>
<li>Implementujte u příkazů <code>mole [-m] [FILTERS] [DIRECTORY]</code>
a <code>list</code> nový přepínač <code>-d</code> (default), který
způsobí, že <code>mole</code> bude pracovat pouze se záznamy spuštění
(editace) souborů bez specifikované skupiny.
<ul>
<li>Tedy např. při použití příkazu <code>mole -d ~</code> bude ignorován
záznam o spuštění <code>mole -g bash ~/.bashrc</code>.</li>
<li>Přepínač <code>-d</code> bude výlučný s přepínačem <code>-g</code>,
tedy v rámci jednoho spuštění <code>mole</code> nemohou být zadány oba
přepínače zároveň.</li>
</ul></li>
<li>Implementace přepínačů <code>-d</code> a <code>-r</code> je
nepovinná; korektní implementace může vynahradit jiné bodové
ztráty.</li>
</ul>
<h1 id="odevzdávání">Odevzdávání</h1>
<p>Odevzdávejte pouze skript <code>mole</code> (nebalte ho do žádného
archivu) do IS VUT.</p>
