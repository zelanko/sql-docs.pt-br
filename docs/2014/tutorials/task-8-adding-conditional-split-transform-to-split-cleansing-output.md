---
title: 'Tarefa 8: Adicionar condicional dividir a transformação para dividir a limpeza de saída | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 401768ca9a811e9b9709127be391bb52de778b32
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024337"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>Tarefa 8: Adicionando a Transformação Divisão Condicional para dividir a saída da limpeza
  Nesta transformação, você adiciona uma Transformação Divisão Condicional ao fluxo de dados. A transformação Divisão Condicional pode rotear linhas para saídas diferentes com base no conteúdo dos dados. Para este tutorial, você deve usar o **Status do registro** coluna de saída da transformação limpeza DQS. Apenas os registros corretos ou corrigidos serão carregados no servidor MDS neste tutorial. Portanto, é verificar se o **Status do registro** é **correto** ou **corrigido**e combine os registros antes de carregar os registros no MDS.  
  
1.  Arrastar e soltar **transformação divisão condicional** de **comuns** seção os **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia em **Limpar dados do fornecedor**.  
  
2.  Clique com botão direito **divisão condicional**e clique em **Renomear**. Tipo de **escolher registros corretos e corrigidos** e pressione **ENTER**.  
  
3.  Conectar-se **limpar dados do fornecedor** e **escolher registros corretos e corrigidos** usando o conector azul.  
  
     ![Fornecedor de limpar dados -> escolher correto & corrigido](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "fornecedor de limpar dados -> escolher correto & corrigido")  
  
4.  Clique duas vezes em **escolher registros corretos e corrigidos** na **fluxo de dados** guia.  
  
5.  Alterar o **nome de saída padrão** na parte inferior da tela para **correto**.  
  
6.  Expandir **colunas** na **painel superior esquerdo**.  
  
     ![Editor de transformação de divisão condicional](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "Editor de transformação de divisão condicional")  
  
7.  Arrastar e soltar **Status do registro** para o **condição** coluna.  
  
8.  Tipo de **= = "Corrigido"** lado **[Status do Registro]** para o **condição** coluna.  
  
9. Clique em **caso 1** na **coluna de nome de saída**e altere o nome para **corrigido**.  
  
10. Clique em **Okey** para fechar o **Editor de transformação de divisão condicional** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 9: Adicionando a união transformação tudo para combinar registros corretos e corrigidos](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
