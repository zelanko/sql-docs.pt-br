---
title: Restrições exclusivas e restrições de verificação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], Visual Database Tools
- Visual Database Tools [SQL Server], constraints
ms.assetid: 637098af-2567-48f8-90f4-b41df059833e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2a8dfd7da9bb1ccc60d18e68ccbe4930a6edb00d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196672"
---
# <a name="unique-constraints-and-check-constraints"></a>Restrições exclusivas e restrições de verificação
  Restrições UNIQUE e CHECK são dois tipos de restrições que podem ser usadas para impor a integridade de dados em tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses são objetos de banco de dados importantes.  
  
 Este tópico inclui as seções a seguir.  
  
 [Restrições UNIQUE](#Unique)  
  
 [Restrições CHECK](#Check)  
  
 [Tarefas relacionadas](#Tasks)  
  
##  <a name="Unique"></a> Restrições UNIQUE  
 Restrições são regras que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] impõe a você. Por exemplo, você pode usar as restrições UNIQUE para garantir que não há valores duplicados inseridos em colunas específicas que não participam de uma chave primária. Embora a restrição UNIQUE e a restrição PRIMARY KEY impõem exclusividade, use a restrição UNIQUE em vez da restrição PRIMARY KEY quando for impor a exclusividade de uma coluna, ou uma combinação de colunas, que não seja uma chave primária.  
  
 Diferente das restrições PRIMARY KEY, as restrições UNIQUE permitem o valor NULL. Porém, como com qualquer valor que participa de uma restrição UNIQUE, só um valor nulo é permitido por coluna. Uma restrição UNIQUE pode ser referenciada por uma restrição FOREIGN KEY.  
  
 Quando uma nova restrição UNIQUE é adicionada a uma coluna ou colunas existentes em uma tabela, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] , por padrão, examina os dados existentes nas colunas para certificar-se de que todos os valores são únicos. Se uma restrição UNIQUE for adicionada a uma coluna que tem valores duplicados, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] retornará um erro e não adicionará a restrição.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria automaticamente um índice UNIQUE para impor a exclusividade do requisito da restrição UNIQUE. Portanto, se houver uma tentativa de inserir uma linha duplicada, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] retornará uma mensagem de erro indicando que a restrição UNIQUE foi violada e a linha não será adicionada à tabela. A menos que um índice clusterizado seja explicitamente especificado, um índice não clusterizado e único é criado por padrão para impor a restrição UNIQUE.  
  
##  <a name="Check"></a> Restrições CHECK  
 Restrições CHECK impõe integridade de domínio limitando os valores aceitos por uma ou mais colunas. Você pode criar uma restrição CHECK com qualquer expressão lógica (Booleana) que retorne TRUE ou FALSE com base em operadores lógicos. Por exemplo, o intervalo de valores para uma coluna **salário** pode ser limitado pela criação de uma restrição CHECK, que apenas permite que os dados variem entre US$ 15.000 e US$ 100.000. Isto evita que salários sejam digitados além do intervalo de salário regular. A expressão lógica seria a seguinte: `salary >= 15000 AND salary <= 100000`.  
  
 Você pode aplicar várias restrições CHECK a uma única coluna. Você também pode aplicar uma única restrição CHECK a várias colunas criando-as ao nível de tabela. Por exemplo, uma restrição CHECK de várias colunas poderia ser usada para confirmar que qualquer linha com o valor de coluna **country_region** de **USA** também tenha um valor de dois caracteres na coluna **state** . Isto permite que várias condições sejam verificadas em um local.  
  
 Restrições CHECK são semelhantes a restrições FOREIGN KEY pelo fato de controlarem os valores colocados em uma coluna. A diferença está em como elas determinam quais valores são válidos: restrições FOREIGN KEY obtêm uma lista de valores válidos de uma outra tabela, enquanto que restrições CHECK determinam valores válidos de uma expressão lógica.  
  
> [!CAUTION]  
>  Restrições que incluem conversão de tipo de dados implícita ou explícita podem causar falhas em certas operações. Por exemplo, tais restrições definidas em tabelas que são fontes de opção de partição podem causar falha na operação ALTER TABLE...SWITCH. Evite a conversão de tipo de dados em definições de restrição.  
  
### <a name="limitations-of-check-constraints"></a>Limitações de restrições CHECK  
 As restrições CHECK rejeitam valores avaliados como FALSE. Porque valores nulos avaliam a UNKNOWN, a sua presença em expressões pode anular uma restrição. Por exemplo, suponha que você coloque uma restrição em `int` uma coluna **MyColumn** especificando que **MyColumn** pode conter apenas o valor 10 (**MyColumn = 10**). Se você inserir o valor NULL em **MyColumn**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] inserirá NULL e não retornará um erro.  
  
 Uma restrição CHECK retorna TRUE quando a condição que está verificando não é FALSE para qualquer linha na tabela. Uma restrição CHECK funciona no nível de linha. Se a tabela acabou de ser criada e não tiver nenhuma linha, qualquer restrição CHECK nesta tabela é considerada válida. Esta situação pode produzir resultados inesperados, como no exemplo seguinte.  
  
```  
CREATE TABLE CheckTbl (col1 int, col2 int);  
GO  
CREATE FUNCTION CheckFnctn()  
RETURNS int  
AS   
BEGIN  
   DECLARE @retval int  
   SELECT @retval = COUNT(*) FROM CheckTbl  
   RETURN @retval  
END;  
GO  
ALTER TABLE CheckTbl  
ADD CONSTRAINT chkRowCount CHECK (dbo.CheckFnctn() >= 1 );  
GO  
```  
  
 A restrição `CHECK` que está sendo adicionada especifica que deve haver pelo menos uma linha na tabela `CheckTbl`. Entretanto, porque não há nenhuma linha na tabela para a qual verificar a condição desta restrição, a instrução ALTER TABLE têm êxito.  
  
 Restrições CHECK não são validadas durante instruções DELETE. Portanto, executando instruções DELETE em tabelas com certos tipos de restrições de verificação pode produzir resultados inesperados. Por exemplo, considere as instruções a seguir executadas na tabela `CheckTbl`.  
  
```  
INSERT INTO CheckTbl VALUES (10, 10);  
GO  
DELETE CheckTbl WHERE col1 = 10;  
```  
  
 A instrução `DELETE` tem êxito, embora a restrição `CHECK` especifique qual tabela `CheckTbl` deva ter pelo menos `1` linha.  
  
##  <a name="Tasks"></a> Tarefas relacionadas  
  
> [!NOTE]  
>  Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Descreve como criar uma restrição exclusiva.|[Criar restrições exclusivas](../tables/create-unique-constraints.md)|  
|Descreve como modificar uma restrição exclusiva.|[Modificar restrições exclusivas](../tables/modify-unique-constraints.md)|  
|Descreve como excluir uma restrição exclusiva.|[Excluir restrições exclusivas](../tables/delete-unique-constraints.md)|  
|Descreve como desabilitar uma restrição de verificação quando um agente de replicação insere ou atualiza dados em sua tabela.|[Desabilitar verificação de restrições para replicação](../tables/disable-check-constraints-for-replication.md)|  
|Descreve como desabilitar uma restrição de verificação quando dados são adicionados, atualizados ou excluídos de uma tabela.|[Desabilitar restrições de verificação com instruções INSERT e UPDATE](../tables/disable-check-constraints-with-insert-and-update-statements.md)|  
|Descreve como alterar a expressão de restrição ou as opções que habilitam ou desabilitam a restrição para condições específicas.|[Modificar restrições de verificação](../tables/modify-check-constraints.md)|  
|Descreve como excluir uma restrição de verificação.|[Excluir restrições de verificação](../tables/delete-check-constraints.md)|  
|Descreve como exibir as propriedades de uma restrição de verificação.|[Restrições exclusivas e restrições de verificação](../tables/unique-constraints-and-check-constraints.md)|  
  
  
