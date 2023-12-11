# generate_random_key
Vamos documentar a função `generate_random_key` no formato Markdown para o README.md:

# Função para Gerar Chave Aleatória

Esta função PL/SQL, `generate_random_key`, é projetada para gerar uma chave aleatória alfanumérica. A chave gerada possui um comprimento de 20 caracteres e inclui letras maiúsculas, minúsculas e dígitos.

## Função PL/SQL

```sql
CREATE OR REPLACE FUNCTION generate_random_key RETURN VARCHAR2 IS
    v_key VARCHAR2(1000);
    v_char VARCHAR2(1);
    v_random_num NUMBER;
    v_counter NUMBER := 0; -- Contador para adicionar traço a cada 4 caracteres
BEGIN
    v_key := '';
    FOR i IN 1..20 LOOP  -- Largura da chave é 20 caracteres
        -- Gera um número aleatório entre 1 e 36 (26 letras + 10 dígitos)
        v_random_num := CEIL(DBMS_RANDOM.value(1, 36));
        
        -- Converte o número em um caractere alfanumérico
        IF v_random_num <= 26 THEN
            -- Letras (maiúsculas e minúsculas)
            IF DBMS_RANDOM.value(0, 1) < 0.5 THEN
                v_char := CHR(64 + v_random_num); -- Letras maiúsculas
            ELSE
                v_char := CHR(96 + v_random_num); -- Letras minúsculas
            END IF;
        ELSE
            v_char := CHR(47 + (v_random_num - 26)); -- Dígitos
        END IF;
        v_key := UPPER(v_key || v_char); -- Constrói a chave
        -- Adiciona traço a cada 4 caracteres
        v_counter := v_counter + 1;
        IF v_counter = 4 AND i < 20 THEN
            v_key := v_key || '-';
            v_counter := 0;
        END IF;
    END LOOP;
    RETURN v_key;
END generate_random_key;
```

## Uso

Para utilizar esta função, basta chamá-la em uma instrução SQL ou PL/SQL. Por exemplo:

```sql
DECLARE
    nova_chave VARCHAR2(1000);
BEGIN
    nova_chave := generate_random_key();
    DBMS_OUTPUT.PUT_LINE('Nova Chave Aleatória: ' || nova_chave);
END;
```

Este exemplo demonstra como chamar a função `generate_random_key` para obter uma nova chave aleatória.

```

Lembre-se de adaptar a documentação conforme necessário para refletir completamente o contexto e os requisitos específicos do seu projeto.
