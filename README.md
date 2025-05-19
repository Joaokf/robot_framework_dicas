## Keyword: Selecionar Intervalo de Datas

Selecionar datas no calendário (date-picker)

```robotframework
*** Keywords ***
Selecionar Intervalo de Datas
    [Arguments]    ${ano_inicio}    ${mes_inicio}    ${dia_inicio}    ${ano_fim}    ${mes_fim}    ${dia_fim}

    # Abrir o calendário
    Wait Until Element Is Visible    xpath=(//span[@id="dateRange"])[1]    10s
    Click Element                    xpath=(//span[@id="dateRange"])[1]
    Sleep                            1s

    # Selecionar ano e mês do início (como só tem um calendário, será o mesmo para as duas datas)
    Select From List By Value        xpath=//select[@title="Select year"]     ${ano_inicio}
    Select From List By Label        xpath=//select[@title="Select month"]    ${mes_inicio}
    Sleep                            1s

    # Clicar na data de início
    Click Element    xpath=(//span[contains(@class, 'custom-day') and not(contains(@class, 'disabled')) and normalize-space()='${dia_inicio}'])[1]
    Sleep            1s

    # Se for o mesmo mês/ano, clique na segunda data diretamente
    Click Element    xpath=(//span[contains(@class, 'custom-day') and not(contains(@class, 'disabled')) and normalize-space()='${dia_fim}'])[last()]
    Sleep            2s


## Como Usar:
No seu Test Case, basta chamá‑lo passando as datas de início e fim:

*** Test Cases ***
Exemplo de Seleção de Intervalo
    Selecionar Intervalo de Datas    2024    Abr    1    2025    Mai    1

Isso abrirá o calendário, ajustará o ano e o mês, e marcará 01/Abr/2024 como data inicial e 01/Mai/2025 como data final, tudo em um único painel.
