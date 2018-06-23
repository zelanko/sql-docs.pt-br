---
title: Gatilhos DML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], about triggers
- DML triggers, about DML triggers
- triggers [SQL Server]
ms.assetid: 298eafca-e01f-4707-8c29-c75546fcd6b0
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b13c888a8f3a388d6e1b8d1b2763714c9558004a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130930"
---
# <a name="dml-triggers"></a>Gatilhos DML
  Os gatilhos DML são um tipo especial de procedimento armazenado que entra em vigor automaticamente quando um evento DML (linguagem de manipulação de dados) ocorre e afeta a tabela ou exibição definida no gatilho. Os eventos DML são instruções INSERT, UPDATE ou DELETE. Os gatilhos DML podem ser usados para impor regras de negócios e integridade de dados, consultar outras tabelas e incluir instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] complexas. O gatilho e a instrução que o dispara são tratados como uma transação simples, que pode ser revertida dentro do gatilho. Se um erro grave for detectado (espaço em disco insuficiente, por exemplo), toda a transação será revertida automaticamente.  
  
## <a name="dml-trigger-benefits"></a>Benefícios do gatilho DML  
 Os gatilhos DML são semelhantes a restrições, pois podem impor integridade de entidade ou integridade de domínio. Em geral, a integridade da entidade sempre deve ser imposta no menor nível por índices que fazem parte das restrições PRIMARY KEY e UNIQUE ou que são criados independentemente de restrições. A integridade de domínio deve ser imposta por restrições CHECK e a RIN (integridade referencial) deve ser imposta por restrições FOREIGN KEY. Os gatilhos DML são muito úteis quando os recursos suportados por restrições não atendem às necessidades funcionais do aplicativo.  
  
 A lista a seguir compara gatilhos DML com restrições e identifica quando os gatilhos DML mais benefícios que ela.  
  
-   Os gatilhos DML podem colocar as alterações em cascata através das tabelas relacionadas no banco de dados; no entanto, essas alterações podem ser executadas com mais eficiência utilizando restrições de integridade referencial em cascata. As restrições FOREIGN KEY só podem validar um valor de coluna com uma combinação exata de valor em outra coluna a menos que a cláusula REFERENCES defina uma ação referencial em cascata.  
  
-   Podem proteger contra operações mal-intencionadas ou incorretas do tipo INSERT, UPDATE, e DELETE, e fazer cumprir as outras restrições mais complexas do que aquelas definidas nas restrições CHECK.  
  
     Diferentemente das restrições CHECK, os gatilhos DML podem fazer referência a colunas em outras tabelas. Por exemplo, um gatilho pode usar um SELECT de outra tabela para comparar com os dados atualizados ou inseridos e para efetuar ações adicionais, como modificar os dados ou exibir uma mensagem de erro definida pelo usuário.  
  
-   Podem avaliar o estado de uma tabela antes e depois da modificação dos dados e efetuar ações com base nessa diferença.  
  
-   Vários gatilhos DML do mesmo tipo (INSERT, UPDATE, ou DELETE), em uma tabela, permitem que múltiplas ações diferentes ocorram em resposta à mesma instrução de modificação.  
  
-   Restrições só podem comunicar erros através de mensagens de erro padronizadas do sistema. Se o aplicativo exigir ou beneficiar-se de mensagens personalizadas e tratamento de erros mais complexo, é necessário usar um gatilho.  
  
-   Gatilhos DML podem desabilitar ou reverter alterações que violam a integridade referencial, cancelando assim a tentativa de modificação de dados. Pode ser que tais gatilhos só tenham efeito ao alterar uma chave estrangeira e se o novo valor não combinar com sua chave primária. Porém, as restrições FOREIGN KEY normalmente são usadas com este propósito.  
  
-   Se houver restrições na tabela de gatilhos, elas serão verificadas após a execução do gatilho INSTEAD OF, mas antes da execução do gatilho AFTER. Se as restrições forem violadas, as ações do gatilho INSTEAD OF serão revertidas e o gatilho AFTER não será executado.  
  
## <a name="types-of-dml-triggers"></a>Tipos de gatilhos DML  
 Gatilho AFTER  
 Os gatilhos AFTER são executados depois que a ação das instruções INSERT, UPDATE, MERGE ou DELETE é executada. Os gatilhos AFTER jamais são executados em caso de uma violação de restrição; por isso, estes gatilhos não podem ser usados em processamentos que possam evitar as violações de restrição. Para cada ação INSERT, UPDATE ou DELETE especificada em uma instrução MERGE, o gatilho correspondente é disparado para cada operação DML.  
  
 Gatilho INSTEAD OF  
 Os gatilhos INSTEAD OF substituem as ações padrão da instrução de gatilho. Portanto, eles podem ser usados para executar uma verificação de erro ou valor em uma ou mais colunas, e executar ações adicionais antes de inserir, atualizar ou excluir uma ou mais linhas. Por exemplo, quando o valor que estiver sendo atualizado em uma coluna de salário calculado por hora, de uma tabela de folha de pagamento, exceder um valor especificado, um gatilho poderá ser definido para produzir uma mensagem de erro e reverter a transação, ou inserir um novo registro em uma trilha de auditoria, antes de inserir o registro na tabela de folha de pagamento. A principal vantagem dos gatilhos INSTEAD OF é que eles habilitam exibições que não seriam atualizáveis para oferecer suporte a atualizações. Por exemplo, uma exibição baseada em várias tabelas base deve usar um gatilho INSTEAD OF para oferecer suporte a inserções, atualizações e exclusões que referenciam dados em mais de uma tabela. Outra vantagem dos gatilhos INSTEAD OF é que eles o habilitam a codificar lógica que pode rejeitar partes de um lote e, ao mesmo tempo, permitir que outras partes do lote tenham êxito.  
  
 Esta tabela compara a funcionalidade dos gatilhos AFTER e INSTEAD OF.  
  
|Função|Gatilho AFTER|Gatilho INSTEAD OF|  
|--------------|-------------------|------------------------|  
|Aplicabilidade|Tabelas|Tabelas e exibições|  
|Quantidade por tabela ou exibição|Múltiplas ações por ação de gatilho (UPDATE, DELETE e INSERT)|Uma ação por ação de gatilho (UPDATE, DELETE e INSERT)|  
|Referências em cascata|Nenhuma restrição se aplica|Os gatilhos INSTEAD OF UPDATE e DELETE não são permitidos em tabelas que são destinos de restrições de integridade referencial em cascata.|  
|Execução|Após:<br /><br /> Processamento da restrição<br />Ações referenciais declarativas<br />Criação de tabelas**inserted** e **deleted** <br />A ação de gatilho|Antes: processamento da restrição<br /><br /> Em vez de: a ação de gatilho<br /><br /> Depois: criação de tabelas  **inserted** e **deleted**|  
|Ordem de execução|A primeira e a última execução podem ser especificadas|Não aplicável|  
|`varchar(max)`, `nvarchar(max)`, e `varbinary(max)` referências de coluna no **inserido** e **excluído** tabelas|Allowed (permitido)|Allowed (permitido)|  
|`text`, `ntext`, e `image` referências de coluna no **inserido** e **excluído** tabelas|Não permitido|Allowed (permitido)|  
  
 Gatilhos CLR  
 Um gatilho CLR pode ser um gatilho AFTER ou INSTEAD OF. Um gatilho CLR também pode ser um gatilho DDL. Em vez de executar um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] , um gatilho CLR executa um ou mais métodos gravados em código gerenciado que são membros de um assembly criado no .NET Framework e carregado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Descreve como criar um gatilho DML.|[Criar gatilhos DML](create-dml-triggers.md)|  
|Descreve como criar um gatilho CLR.|[Criar gatilhos CLR](create-clr-triggers.md)|  
|Descreve como criar um gatilho DML para tratar modificações de dados de linha única e de várias linhas.|[Crie gatilhos DML para tratar várias linhas de dados](create-dml-triggers-to-handle-multiple-rows-of-data.md)|  
|Descreve como aninhar gatilhos.|[Criar gatilhos aninhados](create-nested-triggers.md)|  
|Descreve como especificar a ordem na qual são os gatilhos AFTER são disparados.|[Especificar o primeiro e o último gatilhos](specify-first-and-last-triggers.md)|  
|Descreve como usar as tabelas especiais inseridas e excluídas no código de gatilho.|[Usar as tabelas inseridas e excluídas](use-the-inserted-and-deleted-tables.md)|  
|Descreve como modificar ou renomear um gatilho DML.|[Modificar ou renomear gatilhos DML](modify-or-rename-dml-triggers.md)|  
|Descreve como exibir informações sobre gatilhos DML.|[Obter informações sobre gatilhos DML](get-information-about-dml-triggers.md)|  
|Descreve como excluir ou desabilitar gatilhos DML.|[Excluir ou desabilitar gatilhos DML](delete-or-disable-dml-triggers.md)|  
|Descreve como gerenciar a segurança do gatilho.|[Gerenciar a segurança dos gatilhos](manage-trigger-security.md)|  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [Funções de gatilho &#40;Transact-SQL&#41;](/sql/t-sql/functions/trigger-functions-transact-sql)  
  
  
