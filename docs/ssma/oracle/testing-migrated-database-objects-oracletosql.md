---
title: Testando migrados objetos de banco de dados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: da2327f94062d81a9b80e1884deb5150be494faa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="testing-migrated-database-objects-oracletosql"></a>Testando migrados objetos de banco de dados (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Assistente de migração para o Oracle Tester (SSMA Tester) testa automaticamente a conversão do objeto de banco de dados e a migração de dados feitas pelo SSMA. Depois que todas as etapas de migração do SSMA estiverem concluídas, use o SSMA testador para verificar objetos convertidos funcionam da mesma forma e que todos os dados foi transferido corretamente.  
  
Você pode testar os seguintes tipos de objeto com o SSMA testador:  
  
-   Tabelas  
  
-   Procedimentos armazenados, inclusive procedimentos empacotados.  
  
-   Funções definidas pelo usuário, incluindo funções empacotadas.  
  
-   Exibições.  
  
-   Instruções de autônomo.  
  
O SSMA Tester executa objetos selecionados para teste no Oracle e suas contrapartes na [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Depois disso, ele compara os resultados de acordo com os critérios a seguir:  
  
-   As alterações nos dados de tabela são idênticos?  
  
-   Os valores de parâmetros de saída para procedimentos e funções são idênticos?  
  
-   Funções retornam os mesmos resultados?  
  
-   São que os conjuntos de resultados idêntico?  
  
> [!NOTE]  
> Atenção! Nunca use SSMA testador em sistemas de produção. Durante a execução de teste, o esquema de origem e os dados são modificados. Enquanto isso, a restauração completa do estado original pode ser impossível para alguns tipos de código testado.  
  
## <a name="prerequisites"></a>Prerequisites  
Se você quiser usar o testador SSMA, instale o pacote de extensão do SSMA Oracle com o **instalar o banco de dados Tester** opção ativada.  
  
Para habilitar a comparação dos dados da tabela resultante, definir o **coluna ROWID gerar** opção para **Sim** antes de inicia a conversão do esquema. O SSMA adicionará uma coluna ROWID para todas as tabelas durante a execução do **converter esquema** comando.  
  
Além disso, verifique o seguinte:  
  
-   Ferramentas de cliente Oracle estão instaladas no computador onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é executado.  
  
-   Integração do Common Language Runtime (CLR) foi habilitada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mecanismo de banco de dados.  
  
Observe que a versão atual do SSMA Tester não suporta a execução paralela por usuários diferentes no mesmo servidor de origem ou de destino.  
  
## <a name="getting-started"></a>Introdução  
[Criar casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Instalando componentes do SSMA no SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
