---
title: Criar um grupo de carga de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
ms.assetid: 072868ec-ceff-4db6-941b-281af731a067
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1cd3b72418d0791d70d28d2dca0a434190a2d4a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68198922"
---
# <a name="create-a-workload-group"></a>Criar um grupo de carga de trabalho
  Você pode criar um grupo de cargas de trabalho usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   **Antes de começar:**  [Limitações e Restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para criar um grupo de carga de trabalho usando:**  [SQL Server Management Studio](#CreWGProp), [Transact-SQL](#CreWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 A memória consumida pela criação de índice na tabela particionada desalinhada é proporcional ao número de partições envolvidas. Se a memória total necessária exceder o limite por consulta (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto pela configuração de grupo de cargas de trabalho, poderá ocorrer uma falha na criação do índice. Como o grupo de cargas de trabalho padrão permite que uma consulta exceda o limite por consulta com o mínimo de memória requerida para iniciar, para compatibilidade com o SQL Server 2005, o usuário talvez possa executar a mesma criação de índice no grupo de cargas de trabalho padrão caso o pool de recursos padrão tenha memória total suficiente configurada para executar tal consulta.  
  
 A criação de índice pode usar mais workspace de memória do que aquela inicialmente concedida a fim de melhorar o desempenho. Esse tratamento especial tem suporte do Administrador de Recursos. No entanto, a concessão inicial e qualquer concessão de memória adicional estão limitadas pelas configurações de pool de recursos e de grupo de cargas de trabalho.  
  
###  <a name="Permissions"></a> Permissões  
 Criar um grupo de cargas de trabalho exige permissão CONTROL SERVER.  
  
##  <a name="CreWGProp"></a> Criar um grupo de cargas de trabalho usando o SQL Server Management Studio  
 **Para criar um grupo de cargas de trabalho usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  No Pesquisador de Objetos, expanda recursivamente o nó **Gerenciamento** para baixo e incluindo o pool de recursos que contém o grupo de cargas de trabalho a ser modificado.  
  
2.  Clique com o botão direito do mouse na pasta **Grupos de Cargas de Trabalho** e clique em **Novo Grupo de Cargas de Trabalho**.  
  
3.  Na grade **Pools de recursos** , verifique se o pool de recursos onde você deseja adicionar o grupo de cargas de trabalho está realçado.  
  
4.  A grade **Grupos de cargas de trabalho para pool de recursos** terão uma nova linha com um nome em branco e valores padrão nas outras colunas.  
  
5.  Clique na célula **Nome** e insira o nome do grupo de cargas de trabalho.  
  
6.  Clique ou clique duas vezes em outras células na linha que você quer alterar das configurações padrão e insira os novos valores.  
  
7.  Para salvar as alterações, clique em **OK**  
  
##  <a name="CreWGTSQL"></a> Criar grupo de cargas de trabalho usando Transact-SQL  
 **Para criar um grupo de cargas de trabalho usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Execute a instrução CREATE WORKLOAD GROUP que especifica os valores de propriedade a serem definidos.  
  
2.  Execute a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O exemplo a seguir cria um grupo de cargas de trabalho chamado `groupAdhoc` no pool de recursos chamado `poolAdhoc`.  
  
```  
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](resource-governor.md)   
 [Habilitar Administrador de Recursos](enable-resource-governor.md)   
 [Criar um pool de recursos](create-a-resource-pool.md)   
 [Alterar as configurações de grupo de carga de trabalho](change-workload-group-settings.md)   
 [Criar e testar uma função de classificação definida pelo usuário](create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
