---
title: "Verificações de consistência do sistema de tabela temporal | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ec081d42-57e4-43c7-9e1c-317ba8f23437
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb67454080657b99983e33e4c46858124b735433
ms.lasthandoff: 04/11/2017

---
# <a name="temporal-table-system-consistency-checks"></a>Verificações de consistência do sistema de tabela temporal
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ao usar tabelas temporais, o sistema realiza uma série de verificações de consistência para garantir que o esquema esteja em conformidade com os requisitos de tempo, e os dados sejam consistentes e permaneçam consistentes. Além disso, as verificações de tempo foram adicionadas à instrução **DBCC CHECKCONSTRAINTS** .  
  
## <a name="system-consistency-checks"></a>Verificações de consistência do sistema  
 Antes que **SYSTEM_VERSIONING** seja definido como **ON**, um conjunto de verificações é executado na tabela de histórico e na tabela atual. Essas verificações são agrupadas em verificações de esquema e verificações de dados (se a tabela de histórico não estiver vazia). Além disso, o sistema também executa uma verificação de consistência do tempo de execução.  
  
### <a name="schema-check"></a>Verificação do esquema  
 Ao criar ou alterar uma tabela para se tornar uma tabela temporal, o sistema verifica se os requisitos foram atendidos:  
  
1.  Os nomes e o número de colunas é o mesmo na tabela atual e na tabela de histórico.  
  
2.  Os tipos de dados correspondem a cada coluna entre a tabela atual e a tabela de histórico.  
  
3.  As colunas de período são definidas como **NOT NULL**.  
  
4.  A tabela atual tem uma restrição de chave primária e a tabela de histórico não tem uma restrição de chave primária.  
  
5.  Nenhuma coluna **IDENTITY** é definida na tabela de histórico.  
  
6.  Nenhum gatilho é definido na tabela de histórico.  
  
7.  Nenhuma chave estrangeira é definida na tabela de histórico.  
  
8.  Nenhuma restrição de tabela ou coluna é definida na tabela de histórico. No entanto, são permitidos valores de coluna padrão na tabela de histórico.  
  
9. A tabela de histórico não é colocada em um grupo de arquivos somente leitura.  
  
10. A tabela de histórico não está configurada para controle de alterações ou captura de dados de alteração.  
  
### <a name="data-consistency-check"></a>Verificação da consistência de dados  
 Antes que **SYSTEM_VERSIONING** seja definido como **ON** e como parte de qualquer operação DML, o sistema executa a seguinte verificação: **SysEndTime** ≥**SysStartTime**  
  
 Ao criar um link para uma tabela de histórico existente, você pode optar por executar uma verificação de consistência de dados. Essa verificação de consistência de dados garante que os registros existentes não se sobreponham e que exigências de tempo sejam cumpridas para cada registro individual. A execução da verificação de consistência dos dados é o padrão. Em geral, a execução da consistência de dados é recomendável sempre que os dados entre as tabelas atual e histórico possam estar fora de sincronia, por exemplo, ao incorporar uma tabela de histórico existente que é preenchida com dados de histórico.  
  
> [!WARNING]  
>  Alterações manuais ao relógio do sistema farão com que o sistema falhe inesperadamente porque as verificações de consistência de dados de tempo de execução que estão em vigor para evitar condições de sobreposição (ou seja, que a hora de término de um registro não seja anterior à hora de início) falharão.  
  
## <a name="dbcc-checkconstraints"></a>DBCC CHECKCONSTRAINTS  
 O comando **DBCC CHECKCONSTRAINTS** inclui verificações de consistência de dados temporais. Para obter mais informações, veja [DBCC CHECKCONSTRAINTS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md).  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20System%20Consistency%20Checks%20page)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Particionamento de Tabelas Temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

