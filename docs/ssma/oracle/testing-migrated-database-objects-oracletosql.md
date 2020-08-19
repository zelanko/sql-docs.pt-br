---
description: Testar objetos de banco de dados migrados (OracleToSQL)
title: Testando objetos de banco de dados migrados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: ffc8a0d83bac1ca6e08b3f42bf8fda82aa3555a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468847"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>Testar objetos de banco de dados migrados (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Assistente de Migração para Oracle Tester (SSMA Tester) testa automaticamente a conversão de objetos de banco de dados e a migração feita pelo SSMA. Depois que todas as etapas de migração do SSMA forem concluídas, use o SSMA Tester para verificar se os objetos convertidos funcionam da mesma maneira e se todos os dados foram transferidos corretamente.  
  
Você pode testar os seguintes tipos de objeto com o SSMA Tester:  
  
-   Tabelas  
  
-   Procedimentos armazenados, incluindo procedimentos empacotados.  
  
-   Funções definidas pelo usuário, incluindo funções empacotadas.  
  
-   Exibições.  
  
-   Instruções autônomas.  
  
O SSMA Tester executa objetos selecionados para teste no Oracle e em suas contrapartes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Depois disso, ele compara os resultados de acordo com os seguintes critérios:  
  
-   As alterações nos dados da tabela são idênticas?  
  
-   Os valores dos parâmetros de saída para procedimentos e funções são idênticos?  
  
-   As funções retornam os mesmos resultados?  
  
-   Os conjuntos de resultados são idênticos?  
  
> [!NOTE]  
> Atenção! Nunca use o SSMA Tester em sistemas de produção. Durante a execução do testador, o esquema de origem e os dados são modificados. Enquanto isso, a restauração completa do estado original pode ser impossível para alguns tipos de código testado.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Se você quiser usar o SSMA Tester, instale o pacote de extensão do SSMA Oracle com a opção **instalar banco de dados do testador** ativada.  
  
Para habilitar a comparação dos dados da tabela resultante, defina a opção **gerar coluna de ROWID** como **Sim** antes do início da conversão do esquema. O SSMA adicionará uma coluna de ROWID a todas as tabelas durante a execução do comando **converter esquema** .  
  
Além disso, verifique o seguinte:  
  
-   As ferramentas de cliente Oracle são instaladas no computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado.  
  
-   A integração CLR (Common Language Runtime) foi habilitada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados.  
  
Observe que a versão atual do SSMA Tester não oferece suporte à execução paralela por diferentes usuários no mesmo servidor de origem ou de destino.  
  
## <a name="getting-started"></a>Introdução  
[Criando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Instalando os componentes do SSMA em SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
