# Gerador de Horários Escolares

Este projeto implementa um gerador de horários escolares utilizando a biblioteca **OR-Tools** do Google para resolver problemas de otimização. O objetivo é criar uma grade horária que atenda às necessidades das turmas, respeitando as restrições de disciplinas, professores e horários disponíveis.

## Funcionalidades

- Geração automática de horários para várias turmas.
- Alocação de disciplinas com base na carga horária necessária por turma.
- Respeito às restrições de disponibilidade de professores e suas disciplinas.
- Compatibilidade com diferentes dias e horários da semana.

---

## Estrutura do Projeto

### 1. **Definição dos Dados**

- **Turmas**: Lista de turmas que precisam de horários.
  ```python
  turmas = ["1º A", "1º B", "1º C", "1º D", "2º A HUM", "2º B EXAT", "3º A HUM"]
  ```

- **Dias e Horários**: Dias da semana e intervalos disponíveis.
  ```python
  dias = ["Seg", "Ter", "Qua", "Qui", "Sex"]
  horarios = ["14:20 - 15:10", "15:10 - 16:00", ..., "20:30 - 21:20"]
  ```

- **Disciplinas por Turma**: Cada turma possui uma lista de disciplinas e a quantidade de aulas necessárias por semana.
  ```python
  aulas_necessarias = {
      "1º A": {"Matematica": 4, "Portugues": 4, ..., "Ingles": 2},
      ...
      "3º A HUM": {"AMD": 2, "Filosofia": 2, ..., "Redação": 2}
  }
  ```

- **Professores**: Cada professor está associado a disciplinas específicas e possui um limite máximo de aulas por semana.
  ```python
  professores = {
      "LINCOLN": ["Matematica", "OE", "Eletiva"],
      ...
      "ADRIELI": ["Sociologia", "Eletivas"]
  }
  
  aulas_maximas = {
      "LINCOLN": 30,
      ...
      "ADRIELI": 30
  }
  ```

---

### 2. **Modelo Matemático**

O projeto utiliza o **CP-SAT Solver** da OR-Tools para modelar o problema como um problema de satisfação de restrições (CSP).

#### Variáveis:
Cada combinação de turma, dia, horário, disciplina e professor é representada por uma variável booleana:
```python
horario_disciplina[(turma, dia, horario, disciplina, professor)] = model.NewBoolVar(...)
```

#### Restrições:
1. Cada turma deve ter apenas uma disciplina alocada em cada horário.
2. Um professor não pode estar em mais de uma turma no mesmo horário.
3. A carga horária semanal total de cada professor não pode exceder seu limite máximo.
4. Todas as disciplinas devem ser alocadas conforme a carga horária necessária.

---

### 3. **Execução do Programa**

O programa realiza os seguintes passos:

1. **Cálculo Inicial**:
   - Total de horários disponíveis por semana.
   - Total de aulas necessárias para preencher todas as turmas.
   ```python
   total_horarios = len(dias) * len(horarios)
   total_aulas = sum(sum(d.values()) for d in aulas_necessarias.values())
   print(f"Total de horários: {total_horarios}, Total de aulas necessárias: {total_aulas}")
   ```

2. **Criação do Modelo**:
   - Definição das variáveis e restrições.

3. **Solução**:
   - Uso do solver para encontrar uma solução viável ou indicar que nenhuma solução é possível.

4. **Exibição dos Resultados**:
   - Impressão dos horários gerados para cada turma em formato tabular.

---

### Exemplo de Saída

Para a turma `1º A`, o programa gera uma tabela como esta:

| Dia       | Horário         | Disciplina          | Professor     |
|-----------|-----------------|---------------------|---------------|
| Segunda   | 14:20 - 15:10   | Ed. Fin             | LUCA          |
| Segunda   | 15:10 - 16:00   | Matemática          | LINCOLN       |
| ...       | ...             | ...                 | ...           |

---

## Requisitos

### Dependências
- Python (>=3.8)
- OR-Tools
- Pandas

### Instalação
1. Clone o repositório:
   ```bash
   git clone 
   cd 
   ```
2. Instale as dependências:
   ```bash
   pip install ortools pandas
   ```

3. Execute o script principal:
   ```bash
   python main.py
   ```

---

## Limitações Conhecidas

- Não considera intervalos ou períodos livres entre as aulas.
- Não implementa preferências individuais dos professores ou turmas.

---

## Contribuição

Sinta-se à vontade para abrir issues ou enviar pull requests com melhorias.

Citations:
[3] https://www.alura.com.br/artigos/como-publicar-seu-codigo-python-no-pypi
[4] https://www.amandanascimento.com/post/criar-arquivo-readme-md
[5] https://github.com/alura-cursos/readme-template
[6] https://www.alura.com.br/artigos/escrever-bom-readme
[7] https://github.com/alura-cursos/readme-template/activity
[8] https://cursos.alura.com.br/forum/topico-readme-md-meu-perfil-478477
[9] https://cursos.alura.com.br/forum/topico-readme-md-em-empresas-319441
[10] https://www.alura.com.br/artigos/criando-repositorio-remoto-github
[11] https://cursos.alura.com.br/forum/topico-duvida-badge-da-alura-para-meu-readme-352882
[12] https://www.alura.com.br/artigos/o-que-e-git-github
[13] https://cursos.alura.com.br/forum/topico-git-hub-criando-um-readme-220941
[14] https://cursos.alura.com.br/forum/topico-duvida-como-colocar-um-projeto-na-vitrine-dev-360130
[15] https://github.com/andreepdias/curso-alura-docker/blob/main/README.md
[16] https://www.alura.com.br/artigos/clonando-repositorio-git-github
[17] https://www.alura.com.br/conteudo/git-github-dominando-controle-versao-codigo
[18] https://www.alura.com.br/artigos/design-patterns-introducao-padroes-projeto
[19] https://www.alura.com.br/artigos/portfolio-em-dados
[20] https://www.reddit.com/r/learnprogramming/comments/vxfku6/how_to_write_a_readme/
[21] https://www.alura.com.br/artigos/como-criar-um-readme-para-seu-perfil-github
[22] https://www.youtube.com/watch?v=TsaLQAetPLU
