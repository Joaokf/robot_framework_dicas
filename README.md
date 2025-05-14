## Keyword: Selecionar Intervalo de Datas

Opens the ng‑bootstrap datepicker once and selects both a start and end date in the **same** calendar panel via JavaScript, without closing/reopening between selections.

```robotframework
*** Keywords ***
Selecionar Intervalo de Datas
    [Arguments]    ${ano_inicio}    ${mes_inicio}    ${dia_inicio}    ${ano_fim}    ${mes_fim}    ${dia_fim}

    # 1) Abrir o calendário
    Wait Until Element Is Visible    xpath=(//span[@id="dateRange"])[1]    10s
    Click Element                    xpath=(//span[@id="dateRange"])[1]
    Sleep                            1s

    # 2) Selecionar ano/mês (afeta ambos os meses exibidos)
    Select From List By Value        xpath=(//select[@title="Select year"])[1]     ${ano_inicio}
    Select From List By Label        xpath=(//select[@title="Select month"])[1]    ${mes_inicio}
    Sleep                            1s

    # 3) Clicar data inicial e final no mesmo painel via JS (uma única linha)
    Execute JavaScript    var days=Array.from(document.querySelectorAll("span.custom-day:not(.disabled)")); var start=days.find(d=>d.textContent.trim()==="${dia_inicio}"); if(start) start.parentNode.click(); var end=days.reverse().find(d=>d.textContent.trim()==="${dia_fim}"); if(end) end.parentNode.click();
    Sleep                            2s
