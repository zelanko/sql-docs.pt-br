---
title: Configurações globais (testador) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0070dbed0b683b37c0280b9948ff4b592fea9084
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029003"
---
# <a name="global-settings-tester-sybasetosql"></a>Configurações globais (testador) (SybaseToSQL)
Use a página testador da caixa de diálogo **configurações globais** para especificar as configurações para o SSMA Tester.  
  
Para acessar as configurações do testador, no menu **ferramentas** , selecione **configurações globais**e clique em **testador** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Análise de objeto testada**  
Essa configuração especifica se a análise dos objetos de teste deve ser executada. Selecione **Sim** se você quiser que o SSMA Tester analise e verifique automaticamente os objetos dependentes. A opção padrão definida é **Sim**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
**Modo de salvamento de tabelas auxiliares**  
Essa configuração especifica como salvar as tabelas auxiliares internas criadas durante a execução do caso de teste. As opções a seguir podem ser definidas para essa configuração específica:  
  
1.  Sempre excluir  
  
2.  Sempre salvar  
  
3.  Salvar se a comparação de tabelas falhou  
  
4.  Perguntar ao usuário se a comparação da tabela falhou  
  
O conjunto de opções padrão é: **sempre excluir**.  
  
**Executar reversão de dados**  
Essa configuração especifica se uma operação de reversão deve ser executada após a execução de cada caso de teste. O conjunto de opções padrão é **não**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
**Parar a execução do teste após a primeira falha**  
Essa configuração especifica se o caso de teste em execução atual deve ser interrompido, se um erro ocorreu durante a execução. A opção padrão definida é **Sim**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
## <a name="see-also"></a>Consulte Também  
[Concluindo a preparação do caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
