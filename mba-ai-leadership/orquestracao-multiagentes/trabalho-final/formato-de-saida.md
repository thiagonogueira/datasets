# Formato de saída das automações

As duas arquiteturas produzem, para cada chamado, uma saída com os quatro campos abaixo, nesta ordem e com estes rótulos. As ações são simuladas: a automação informa o que faria, sem emitir reembolsos, alterar pedidos ou enviar mensagens a clientes.

```
Chamado: <identificador>

Natureza do chamado: <nome do procedimento aplicado>
<quando a natureza muda durante o atendimento, informar: "Aberto como <natureza informada pelo cliente>; tratado como <natureza aplicada>, porque <motivo>">

Ações, na ordem em que seriam executadas:
1. <ação, com o nome usado no procedimento>
2. <ação>
...

Aprovação do supervisor humano: <Sim ou Não>. Motivo: <valor e limite aplicável, ou "não há reembolso">

Resposta ao cliente:
<texto da resposta, como seria enviado>
```

Regras do formato.

- Cada ação leva o nome usado no procedimento (consultar o rastreio, abrir ocorrência com a transportadora, gerar etiqueta de devolução, suspender o anúncio, pedir a aprovação do supervisor, emitir o reembolso, responder).
- "Pedir a aprovação do supervisor" aparece na lista de ações, na posição em que o procedimento a exige, quando a aprovação é necessária.
- Quando o procedimento manda negar ou encerrar sem ação, a lista de ações contém só as consultas feitas e "responder".
- A resposta ao cliente é coerente com as ações: não promete reembolso que depende de aprovação ainda não dada, nem etiqueta que não foi gerada.
