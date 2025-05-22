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

    # Seletor ano e mês início
    Select From List By Value        xpath=(//select[@title="Select year"])[1]    ${ano_inicio}
    Select From List By Label        xpath=(//select[@title="Select month"])[1]   ${mes_inicio}
    Sleep                            1s

    # Clicar no dia de início pelo aria-label
    Click Element    xpath=(//div[@class="ngb-dp-day"][@aria-label="${dia_inicio}"])[1]
    Sleep            1s

    # Seletor ano e mês fim
    Select From List By Value        xpath=(//select[@title="Select year"])[1]    ${ano_fim}
    Select From List By Label        xpath=(//select[@title="Select month"])[1]   ${mes_fim}
    Sleep                            1s

    # Clicar no dia de fim pelo aria-label
    Click Element    xpath=(//div[@class="ngb-dp-day"][@aria-label="${dia_fim}"])[1]
    Sleep            2s


## Como Usar:
No seu Test Case, basta chamá‑lo passando as datas de início e fim:

*** Test Cases ***
Exemplo de Seleção de Intervalo
    Selecionar Intervalo de Datas    2024    Abr    1    2025    Mai    1

Isso abrirá o calendário, ajustará o ano e o mês, e marcará 01/Abr/2024 como data inicial e 01/Mai/2025 como data final, tudo em um único painel.
