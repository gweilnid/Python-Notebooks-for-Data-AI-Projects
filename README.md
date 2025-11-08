# Python Notebooks for Data & AI Projects

Repozitář obsahuje několik ukázkových notebooků a skript, které demonstrují práci s agentními toky v knihovně [LangGraph](https://www.langchain.com/langgraph) a načítání dat z veřejného API [OpenF1](https://openf1.org/). Každý příklad je zaměřený na jiný typ úlohy – od sekvenčního zpracování stavů přes podmíněné směrování až po smyčky a volání externích služeb. Cílem je ukázat, jak lze Python využít k rychlému prototypování agentních řešení a k práci s daty.

## Co v repozitáři najdete

| Soubor | Popis |
| --- | --- |
| `Langgraph_Sequential.ipynb` | Vytváří jednoduchý sekvenční graf, který postupně skládá textovou odpověď na základě vstupního jména, věku a dovedností uživatele. |
| `Langgraph_loop.ipynb` | Ukázka smyčky v LangGraphu. Agent generuje náhodná čísla, dokud nesplní podmínku ukončení, a průběžně aktualizuje stav. |
| `Lang_Conditional_Graph.ipynb` | Podmíněné směrování mezi uzly. Graf podle zadané operace přepíná mezi sčítáním a odčítáním (ve dvou krocích) a uchovává mezivýsledky. |
| `Lang_agent2.ipynb` | Jednoduchý „single-node" agent, který na základě zvolené operace (+ nebo *) zpracuje seznam čísel a vrací formátovanou odpověď uživateli. |
| `OpenF1.ipynb` | Volání REST API OpenF1. Notebook načte seznam závodů podle země a roku, zjistí výsledky poslední session a dohledá jméno vítězného pilota. |
| `Agent_Bot.py` | Skript s minimální LangGraph aplikací, která využívá `ChatOpenAI` pro jednoduchou konverzaci v terminálu. |

## Rychlý start

1. **Klonování repozitáře**
   ```bash
   git clone https://github.com/gweilnid/Python-Notebooks-for-Data-AI-Projects.git
   cd Python-Notebooks-for-Data-AI-Projects
   ```
2. **Vytvoření virtuálního prostředí (doporučené)**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   ```
3. **Instalace závislostí**
   Většina notebooků využívá knihovny `langgraph`, `langchain`, `langchain-openai`, `python-dotenv`, `requests` a `pandas`.
   ```bash
   pip install langgraph langchain langchain-openai python-dotenv requests pandas
   ```
4. **Spuštění notebooků**
   Notebooky můžete otevřít lokálně přes JupyterLab/Notebook:
   ```bash
   jupyter lab
   ```
   nebo je spustit přímo v Google Colab pomocí odkazů uvedených v horní části jednotlivých notebooků.

## Jak jednotlivé příklady fungují

### LangGraph notebooky
- **Sekvenční tok (`Langgraph_Sequential.ipynb`)** – Tři uzly grafu se volají za sebou a postupně skládají finální zprávu. Ukazuje základní práci se stavem (`TypedDict`) a přechody `add_edge`.
- **Podmíněný graf (`Lang_Conditional_Graph.ipynb`)** – Vstupní stav obsahuje zvolenou operaci. Směrovací uzel (`router`) vyhodnotí, kterou funkci zavolat (sčítání nebo odčítání) a stejná logika se opakuje i ve druhé části grafu.
- **Agent s jedním uzlem (`Lang_agent2.ipynb`)** – Vhodné pro demonstraci jednoduchých transformací dat. Na základě operace se spočítá suma nebo součin a výsledek se vrací v přívětivé větě.
- **Smyčka (`Langgraph_loop.ipynb`)** – Kombinuje podmíněné hrany s počítadlem. Agent generuje náhodné číslo, uloží ho do stavu a podle počtu opakování buď pokračuje ve smyčce, nebo končí.

### OpenF1 notebook
Notebook `OpenF1.ipynb` pracuje s veřejným API. Po zadání země a pozice:
1. Načte seznam závodů v daném roce a vybere příslušný `meeting_key`.
2. Získá výsledky poslední session a vyfiltruje závodníka na požadované pozici.
3. Stáhne referenční seznam jezdců, spojí ho s výsledky a vypíše jméno pilota.

Notebook využívá `requests` pro HTTP dotazy a `pandas` pro základní práci s datovými rámci.

### Terminálový agent
`Agent_Bot.py` demonstruje, jak rychle sestavit jednoduchého konverzačního agenta:
- Načte API klíče z `.env` souboru (`load_dotenv()`).
- Pomocí `StateGraph` vytvoří graf s jedním uzlem `process`, který volá `ChatOpenAI`.
- V konzoli probíhá smyčka `input → odpověď`, dokud uživatel nezadá `exit`.

## Doporučení pro vlastní experimenty
- **Rozšíření stavů:** Přidejte do `TypedDict` další atributy (např. logy, metriky) a sledujte, jak se mění chování grafu.
- **Napojení na další služby:** Podobně jako u OpenF1 můžete snadno napojit další REST API nebo databáze.
- **Vizualizace grafů:** V notebookách se využívá `app.get_graph().draw_mermaid_png()`. Výstup vám pomůže lépe pochopit strukturu a přechody mezi uzly.

## Licenční a etické poznámky
- Při používání OpenAI modelů dbejte na dodržení podmínek služby a bezpečné nakládání s API klíči.
- Data z OpenF1 jsou veřejná, ale respektujte pravidla použití uvedená na stránkách poskytovatele.
