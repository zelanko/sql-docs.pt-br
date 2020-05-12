Descarta um grupo de carga de trabalho do Administrador de Recursos definido pelo usuário existente.

![Ícone de link do tópico](../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe

```syntaxsql
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>Argumentos

*group_name* é o nome de um grupo de carga de trabalho definido pelo usuário existente.

## <a name="remarks"></a>Comentários

A instrução DROP WORKLOAD GROUP não é permitida nos grupos padrão ou internos do Administrador de Recursos.

Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Administrador de Recursos. Para obter mais informações, consulte [Resource Governor](../relational-databases/resource-governor/resource-governor.md).

Se um grupo de carga de trabalho contiver sessões ativas, o descarte ou a movimentação do grupo para um pool de recursos diferente não terá êxito quando a instrução ALTER RESOURCE GOVERNOR RECONFIGURE for chamada para aplicar a alteração. Para evitar esse problema, é possível executar uma das seguintes ações:

- Aguardar até que todas as sessões do grupo afetado sejam desconectadas e depois executar novamente a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.

- Interromper explicitamente as sessões do grupo afetado usando o comando KILL e depois executar novamente a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.

- Reinicie o servidor. Depois que o processo de reinicialização estiver concluído, o grupo excluído não será criado e um grupo movido usará a atribuição do novo pool de recursos.

- Em um cenário no qual você emitiu a instrução DROP WORKLOAD GROUP mas decide que não deseja parar sessões explicitamente para aplicar a mudança, é possível recriar o grupo usando o mesmo nome que ele tinha antes de você emitir a instrução DROP e depois mover o grupo para o pool de recursos original. Para aplicar as alterações, execute a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL SERVER.

## <a name="examples"></a>Exemplos

O seguinte exemplo descarta o grupo de carga de trabalho denominado `adhoc`.

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Consulte Também

- [Resource Governor](../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-governor-transact-sql.md)  