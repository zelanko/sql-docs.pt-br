---
title: Testar objetos de banco de dados (OracleToSQL) migrados | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 771e9a4553679ae2afa0dd58d83b1d15ccf0fd62
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684314"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>Testar objetos de banco de dados migrados (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para o Testador de Oracle (SSMA testador) testa automaticamente a conversão do objeto de banco de dados e a migração de dados feitas por SSMA. Depois que todas as etapas de migração do SSMA estiverem concluídas, use o SSMA testador para verificar objetos convertidos funcionam da mesma maneira e que todos os dados foi transferido corretamente.  
  
Você pode testar os seguintes tipos de objeto com o SSMA testador:  
  
-   Tabelas  
  
-   Procedimentos armazenados, inclusive procedimentos empacotados.  
  
-   Funções definidas pelo usuário, incluindo funções empacotadas.  
  
-   Exibições.  
  
-   Instruções de autônomo.  
  
O SSMA testador executa objetos selecionados para um teste no Oracle e suas contrapartes na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois disso, ele compara os resultados de acordo com os seguintes critérios:  
  
-   As alterações nos dados de tabela são idênticos?  
  
-   Os valores de parâmetros de saída para procedimentos e funções são idênticos?  
  
-   As funções retornam os mesmos resultados?  
  
-   São que os conjuntos de resultados idênticos?  
  
> [!NOTE]  
> Atenção! Nunca use testador SSMA em sistemas de produção. Durante a execução do testador o esquema de origem e os dados são modificados. Enquanto isso, a restauração completa do estado original pode ser impossível para alguns tipos de código testado.  
  
## <a name="prerequisites"></a>Prerequisites  
Se você quiser usar o testador SSMA, instale o pacote de extensão do SSMA Oracle com o **instalar o banco de dados do testador** opção ativada.  
  
Para habilitar a comparação dos dados da tabela resultante, definir a **coluna gerar ROWID** opção **Sim** antes de inicia a conversão de esquema. O SSMA adicionará uma coluna ROWID a todas as tabelas durante a execução do **converter esquema** comando.  
  
Além disso, verifique o seguinte:  
  
-   Ferramentas de cliente Oracle estão instaladas no computador onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado.  
  
-   Integração de Common Language Runtime (CLR) foi habilitada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados.  
  
Observe que a versão atual do testador do SSMA não suporta a execução paralela por usuários diferentes no mesmo servidor de origem ou destino.  
  
## <a name="getting-started"></a>Introdução  
[Criando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Instalar os componentes do SSMA no SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
