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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029003"
---
# <a name="global-settings-tester-sybasetosql"></a>Configurações globais (testador) (SybaseToSQL)
Use a página do testador do **configurações globais** caixa de diálogo para especificar configurações para o testador SSMA.  
  
Para acessar as configurações de testador, sobre o **ferramentas** menu, selecione **configurações globais**e clique em **testador** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Análise de objeto que pode ser testada**  
Essa configuração especifica se deve executar a análise dos objetos que podem ser testados. Selecione **Sim** se você quiser que o Testador de SSMA para analisar e verificar automaticamente os objetos dependentes. É o conjunto de opções padrão **Sim**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
**Tabelas auxiliares do modo de economia**  
Essa configuração especifica como salvar tabelas auxiliares internas criadas durante a execução do caso de teste. Opções a seguir pode ser definida para essa configuração específica:  
  
1.  Sempre excluir  
  
2.  Sempre salvar  
  
3.  Salvar se houve falha na comparação de tabela  
  
4.  Peça ao usuário se houve falha na comparação de tabela  
  
O conjunto de opção padrão é: **Sempre excluir**.  
  
**Executar a reversão de dados**  
Essa configuração especifica se deve executar uma operação de reversão após a execução de cada caso de teste. É o conjunto de opções padrão **não**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
**Parar a execução de teste após a primeira falha**  
Essa configuração especifica se deseja interromper o caso de teste em execução atual, se tiver ocorrido um erro durante a execução. É o conjunto de opções padrão **Sim**.  
  
As seguintes opções estão disponíveis para essa configuração:  
  
1.  Sim  
  
2.  Não  
  
## <a name="see-also"></a>Consulte também  
[Concluir a preparação do caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
