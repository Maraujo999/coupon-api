# Evidências de execução TDD

Registro iniciado em 11/09/2026. Logs completos locais ficam em tmp e não são publicados.

| Ciclo | RED observado antes da implementação | GREEN | Evidência |
| --- | --- | --- | --- |
| Domínio | Compilação sem tipos; após assinaturas: 35 testes, 23 falhas de asserção e 6 erros de operações ainda não implementadas | 35 testes passando | CouponCodeTest, DiscountValueTest, CouponTest; logs domain-red-compile, domain-red e domain-green |
| Casos de uso | Compilação sem tipos; após assinaturas: 11 testes, 7 falhas e 4 erros de operações ainda não implementadas | A verificar | CouponServicesTest; application-red e application-red-assert |

O scaffold veio do Spring Initializr. Corrigido o parent gerado de 4.1.1.RELEASE para 4.1.1, cuja publicação foi confirmada no Maven Central. Nenhuma regra foi implementada no scaffold.
