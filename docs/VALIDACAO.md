# Validação da implementação

Registro da implementação em 11/09/2026. Este arquivo distingue execução local e validação no CI. Os resultados finais são atualizados após as verificações.

## Verificações

- Unitários e testes de integração: Maven Surefire/Failsafe; quantidades e cobertura consolidadas ao concluir o build final.
- Banco real do desafio: H2 em memória com Flyway, validação do schema, decimais grandes/fracionários, precisão temporal, rollback, exclusão lógica e concorrência.
- Segurança: assinatura e claims JWT, 401/403, expiração, token sem assinatura, login e limites.
- HTTP real: 16 verificações contra o JAR, incluindo ciclo completo e respostas inválidas.
- Logs: inspeção automatizada de ERROR, JWT, senha e marcador do corpo de requisição; eventos de criação, exclusão e HTTP obrigatórios.
- Docker/Compose e PIT: executados no runner Linux do GitHub Actions, com resultados a registrar.

## Limitações observadas no ambiente local

O Docker Desktop local falhou ao inicializar o listener de inferência em um socket no AppData. Nenhum dado de container foi removido. A execução do Compose será comprovada separadamente no CI.

A JVM Windows falhou ao abrir um socket temporário sob o AppData durante a inicialização do Tomcat. O helper local aplica `-Djdk.net.unixdomain.tmpdir` ao diretório `tmp` do projeto. Com isso, o JAR iniciou e respondeu às verificações HTTP.

O PIT iniciou no Windows, mas o processo filho não carregou classes de teste no caminho com espaços/acentos. A verificação de mutação foi transferida para o checkout Linux do CI; uma execução abortada não foi contada como sucesso.

## Avisos de inicialização analisados

A execução do JAR emitiu três WARN conhecidos: Flyway informa que o H2 gerenciado pelo Boot é mais novo que sua versão testada; springdoc informa que a documentação JSON e o Swagger UI estão habilitados.

As migrações e o schema foram exercitados com o H2 efetivamente usado. Swagger é um requisito do desafio e fica acessível na demonstração. Os avisos foram mantidos, sem mudar níveis de log para ocultá-los.

Nenhum endpoint de produção foi identificado no Apidog. Todos os testes HTTP reportados se referem à aplicação implementada ou ao container do CI.
