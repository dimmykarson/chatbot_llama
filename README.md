Crie um arquivo .env e adicione sua chave HUGGINGFACEHUB_API_TOKEN

Crie um ambiente virutal com o comando python3 -m venv env
Ative o env: source env/bin/activate
Instale as bibliotecas: pip install -r requirements.txt

Para usuário linux o seguinte código deve ser executado antes de rodar o chat:

__import__('pysqlite3')
import sys
sys.modules['sqlite3'] = sys.modules.pop('pysqlite3')

