# Manual de Triagem de Avisos de Sinistro. AutoProtege (documento fictício)

Categorias e regra de decisão, na ordem de precedência:

1. `nao_coberto`: há na descrição um fato que exclui a cobertura por si só:
   condução sem habilitação válida, uso em competição/racha, transporte
   remunerado de passageiros não declarado, ou embriaguez admitida pelo próprio
   segurado. Precedência sobre qualquer outra categoria.

2. `roubo_furto`: subtração do veículo inteiro, com ou sem violência.
   Se apenas peças ou objetos foram levados, não é esta categoria.

3. `colisao`: impacto do veículo com outro veículo, objeto fixo, animal ou
   capotamento. Se o vidro quebrou como consequência do impacto, continua sendo
   `colisao`. A categoria `vidros` é só para dano de vidro isolado.

4. `vidros`: dano exclusivo a para-brisa, vidro lateral, retrovisor ou
   farol/lanterna, sem impacto estrutural no veículo.

5. `terceiros`: o dano relatado é ao patrimônio ou à integridade de terceiro,
   e o pedido é de acionamento da cobertura de responsabilidade civil.

6. `needs_review`: use quando faltar informação essencial para distinguir entre
   as categorias acima, ou quando o relato for internamente contraditório.
   Não é a categoria para "caso difícil"; é para "não dá para decidir com o que
   está escrito".

Regra de ouro: classifique apenas com base no que está escrito no aviso. Não
suponha circunstâncias que o segurado não relatou.
