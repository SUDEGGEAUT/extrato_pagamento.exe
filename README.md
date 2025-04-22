# README: Automação de Consultas no SIFAMA

## Descrição

Este programa realiza a automação de consultas no sistema **SIFAMA** (Sistema Integrado de Fiscalização e Monitoramento da ANTT), para verificar o status de processos administrativos e salvar os resultados em uma planilha Excel. Além disso, aplica formatação condicional para facilitar a visualização do status de cada processo.

O programa utiliza **Selenium** para automatizar a navegação no site, **Pandas** para manipulação de dados da planilha de entrada, e **openpyxl** para gerar e formatar a planilha de saída.

---

## Funcionalidades

1. **Automação de Login**: Realiza login automático no sistema utilizando as credenciais configuradas.
2. **Consulta de Processos**: Pesquisa os números de processos fornecidos em uma planilha Excel e verifica o status ("Pendente", "Quitada", ou erros).
3. **Registro de Progresso**: Salva localmente os números de processos já processados, evitando duplicidade.
4. **Exportação de Resultados**: Gera uma planilha Excel com os resultados, aplicando formatação condicional para destacar os diferentes status.
5. **Tratamento de Erros**: Detecta e trata erros do sistema ou do servidor, como mensagens de exceção e falhas de carregamento.

---

## Pré-requisitos

### Softwares Necessários
- Python 3.8+ 
- Google Chrome
- Driver do Chrome compatível (chromedriver.exe)

### Bibliotecas Python
Certifique-se de instalar as bibliotecas abaixo antes de executar o programa:
```bash
pip install pymupdf pandas selenium pdf2image pytesseract
```

### Estrutura de Diretórios
- **`chromedriver-win64/chromedriver.exe`**: Caminho onde o driver do Chrome deve estar localizado.
- **`excel/PROCESSO.xlsx`**: Planilha de entrada contendo os números dos processos na coluna `PROCESSO`.

---

## Configuração

1. **Credenciais de Acesso**  
   Atualize as credenciais no método `login_sifama`:
   ```python
   usuario.send_keys("seu_usuario")
   senha.send_keys("sua_senha")
   ```

2. **Caminhos de Arquivos**
   Verifique e ajuste os caminhos configurados no início do script:
   ```python
   chrome_driver_path = os.path.join(atual_dir, "chromedriver-win64", "chromedriver.exe")
   excel_path = os.path.join(atual_dir, "excel", "PROCESSO.xlsx")
   output_excel = os.path.join(atual_dir, "Relatorio.xlsx")
   progresso_path = os.path.join(atual_dir, "progresso.txt")
   log_file = os.path.join(atual_dir, "log_extrato-pagamento.txt")
   ```

---

## Como Usar

1. **Prepare a Planilha de Entrada**  
   Certifique-se de que o arquivo `PROCESSO.xlsx` contém uma coluna chamada `PROCESSO` com os números dos processos a serem pesquisados.

2. **Execute o Programa**  
   No terminal, navegue até o diretório do script e execute:
   ```bash
   python script.py
   ```

3. **Resultados**  
   - Os resultados serão salvos no arquivo `Relatorio.xlsx`.
   - O progresso será registrado no arquivo `progresso.txt`.
   - Logs de execução estarão disponíveis em `log_extrato-pagamento.txt`.

---

## Observações

1. **Login Automático**: Caso o sistema apresente problemas de login, o programa tentará até 3 vezes antes de abortar.
2. **Erros do Sistema**: O programa detecta erros no SIFAMA, como falhas de servidor, e tenta recarregar a página automaticamente.
3. **Progresso Persistente**: Processos já pesquisados não serão repetidos em execuções subsequentes.

---
