# bulkpy

Uma biblioteca Python para transferência em massa de dados para SQL Server usando o utilitário `bcp` (Bulk Copy Program).

## 📋 Descrição

**bulkpy** (bcpy) é uma ferramenta que simplifica a importação de dados de arquivos planos para tabelas SQL Server. Ela encapsula a funcionalidade do `bcp` do SQL Server, oferecendo uma interface Python intuitiva para transferências de dados em massa.

## ✨ Características

- **Transferência em massa de dados**: Importe dados de arquivos planos diretamente para SQL Server
- **Suporte a autenticação Kerberos**: Autenticação segura sem exposição de senhas
- **Autenticação padrão**: Suporte a usuário e senha SQL Server
- **Controle de lote**: Configure o tamanho dos lotes para otimizar performance
- **Objetos de dados flexíveis**: Trabalhe com `FlatFile`, `DataFrame`, `SqlTable` e muito mais
- **Geração automática de formato**: Geração inteligente de arquivos de formato para o `bcp`

## 🚀 Instalação

### Diretamente do GitHub

```bash
pip install git+https://github.com/renatofcesar/bulkpy.git
```

### Para desenvolvimento local

Clone o repositório e instale em modo edição:

```bash
git clone https://github.com/renatofcesar/bulkpy.git
cd bulkpy
pip install -e .
```

## 📦 Requisitos

- Python 3.6+
- SQL Server Tools (bcp utility)
- pandas (para trabalhar com DataFrames)

## 💻 Uso Básico

```python
from bcpy import SqlTable, FlatFile

# Definir a tabela SQL Server
sql_table = SqlTable(
    server='seu_servidor',
    database='sua_database',
    schema='dbo',
    table='sua_tabela',
    username='seu_usuario',
    password='sua_senha'
)

# Definir o arquivo plano
flat_file = FlatFile(
    path='C:/dados/dados.csv',
    delimiter=',',
    qualifier='"',
    file_has_header_line=True
)

# Executar a transferência
from bcpy.binary_callers import bcp
bcp(sql_table, flat_file, batch_size=1000)
```

### Autenticação Kerberos

```python
sql_table = SqlTable(
    server='seu_servidor',
    database='sua_database',
    schema='dbo',
    table='sua_tabela',
    with_krb_auth=True
)
```

## 📁 Estrutura do Projeto

```
bcpy/
├── __init__.py                # Exportações principais
├── binary_callers.py          # Funções que chamam utilitários binários
├── data_objects.py            # Classes de objetos de dados
├── format_file_builder.py     # Construtor de arquivos de formato
└── tmp_file.py                # Gerenciamento de arquivos temporários
```

## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

## 👤 Autor

Renato

---

**Nota**: Este projeto requer que o SQL Server esteja instalado ou acessível na máquina/rede, pois depende do utilitário `bcp`.
