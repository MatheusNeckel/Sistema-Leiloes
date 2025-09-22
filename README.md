# Sistema de Leilões 🏷️

Aplicativo acadêmico em **Java** para gestão de **leilões**: cadastro de usuários (vendedores/compradores), itens/lotes, abertura e encerramento de leilões, registro de **lances** e apuração de vencedor. Interface simples (Swing) e suporte a **CSV** para importação/exportação. Foco em **POO**, camadas e manipulação de arquivos.

## 🎯 Objetivos
- Cadastrar **usuários** (vendedor, comprador) e **itens/lotes**
- Abrir/encerrar **leilões** e definir regras (preço inicial, incremento mínimo)
- Registrar **lances** com validação
- Exportar/Importar dados em **CSV**
- Exercitar arquitetura em camadas e boas práticas

## 🧰 Stack
- Java 17+ (compatível com 11)
- Swing (GUI)
- Ant / Maven / Gradle (qualquer um — ver seção de build)
- Manipulação de arquivos CSV

## ✨ Funcionalidades
- CRUD de usuários e itens/lotes
- Leilões com estados: **rascunho → aberto → encerrado**
- Regras de lance: **valor ≥ lanceAtual + incrementoMínimo**
- Apuração automática do **vencedor** no encerramento
- Importação/Exportação CSV (usuários, itens, leilões, lances)
- Relatório simples de leilões (itens, lances, vencedor)

## 🗂️ Estrutura (sugerida após extrair o zip)
```
/src/...
/data/                 # dados CSV (git-ignored, usar *.example)
docs/                  # capturas de tela, diagramas
/dist/                 # artefatos de build (git-ignored)
```

## ▶️ Como executar

### Opção A) Via NetBeans
1. **Extraia** o conteúdo do `.zip` para a raiz do repositório (ou abra o projeto extraído).
2. Abra no NetBeans e execute o projeto.

### Opção B) Via linha de comando
- **Se houver `build.xml` (Ant):**
  ```bash
  ant clean dist
  ```
- **Se houver `pom.xml` (Maven):**
  ```bash
  mvn -B -DskipTests package
  ```
- **Se houver `build.gradle`:**
  ```bash
  ./gradlew build
  ```
- **Sem ferramenta de build (apenas fontes em `/src`):**
  ```bash
  find src -name "*.java" > sources.txt
  javac -d out @sources.txt
  java -cp out Main
  ```

> **CI**: O GitHub Actions detecta automaticamente Ant/Maven/Gradle. Se só houver `.java`, ele compila “na unha”. Se existir um `.zip` com o projeto, o CI **descompacta antes** de compilar.

## 📄 CSV (padrões sugeridos)

### `data/usuarios.csv`
```
usuario_id,tipo,nome,documento,email,telefone
# tipo: VENDEDOR | COMPRADOR
```

### `data/itens.csv`
```
item_id,titulo,descricao,valor_estimado,vendedor_id
```

### `data/leiloes.csv`
```
leilao_id,item_id,preco_inicial,incremento_minimo,status,data_abertura,data_encerramento,comprador_vencedor_id,valor_final
# status: RASCUNHO | ABERTO | ENCERRADO
```

### `data/lances.csv`
```
lance_id,leilao_id,comprador_id,valor,data_hora
```

- Codificação: UTF-8
- Separador: `,`
- Exemplos em `data/*.csv.example`

## 🛣️ Roadmap
- [ ] Serviços e repositórios por domínio (Usuário, Item, Leilão, Lance)
- [ ] Regras adicionais (reserva, buy-it-now, taxa do vendedor)
- [ ] Testes unitários (JUnit) e mocks
- [ ] Relatórios (PDF/Excel)
- [ ] Persistência opcional com SQLite

## 🤝 Contribuição
Sinta-se à vontade para abrir issues e PRs! Padrões:
- Conventional Commits
- Branches: `feature/*`, `fix/*`
- PR com descrição clara e prints quando relevante

## 📜 Licença
Este projeto é licenciado sob **MIT**. Veja [LICENSE](LICENSE).
