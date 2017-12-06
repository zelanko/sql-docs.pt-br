---
title: "Configurações globais (Tester) (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4acc0f2a-85ba-4c99-856a-89030f5c418e
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 8f539352279a21b6f736616c5425b4f24856cb03
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="global-settings-tester-oracletosql"></a>Configurações globais (Tester) (OracleToSQL)
Use a página de teste do **configurações globais** caixa de diálogo para especificar configurações para o SSMA Tester.  
  
Para acessar as configurações de teste, no **ferramentas** menu, selecione **configurações globais**e clique em **Tester** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Análise de objeto testável**  
Essa configuração especifica se deve executar a análise de objetos podem ser testados. Selecione **Sim** se testador do SSMA para analisar e verificar automaticamente se os objetos dependentes. Conjunto de opção padrão é **Sim**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
**Modo de economia de tabelas auxiliares**  
Essa configuração especifica como salvar tabelas auxiliares internas criadas durante a execução do caso de teste. As opções a seguir pode ser definida para essa configuração específica:  
  
1.  Sempre excluir  
  
2.  Sempre salvar  
  
3.  Salvar se houve falha na comparação de tabela  
  
4.  Peça ao usuário se houve falha na comparação de tabela  
  
O conjunto de opção padrão é: **sempre excluir**.  
  
**Executar reversão de dados**  
Essa configuração especifica se deve executar uma operação de reversão após a execução de cada caso de teste. Conjunto de opção padrão é **não**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
**Interromper a execução de teste após a primeira falha**  
Essa configuração especifica se é preciso parar o caso de teste em execução atual, se tiver ocorrido um erro durante a execução. Conjunto de opção padrão é **Sim**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
## <a name="see-also"></a>Consulte também  
[Concluindo a preparação do caso de teste &#40; OracleToSQL &#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
