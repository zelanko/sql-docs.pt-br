---
title: "Configurações globais (Tester) (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 21178ca7326678504244658192d7395bab79a9ac
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="global-settings-tester-sybasetosql"></a>Configurações globais (Tester) (SybaseToSQL)
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
[Concluindo a preparação do caso de teste &#40; SybaseToSQL &#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  

