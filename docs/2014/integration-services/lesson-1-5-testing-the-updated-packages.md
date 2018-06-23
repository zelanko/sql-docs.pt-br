---
title: 'Etapa 5: testar os pacotes atualizados | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7db13e319b07a605172746a650c0292dc7f2bfd8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010078"
---
# <a name="step-5-testing-the-updated-packages"></a>Etapa 5: Testando os pacotes atualizados
  Antes de ir para a próxima lição, na qual você criará o pacote de implantação a ser usado para instalar os pacotes de tutorial no computador de destino, você deverá testar os pacotes. Nesta tarefa, você executará os pacotes, DataTransfer.dtsx e LoadXMLData que você adicionou ao projeto Tutorial de Implantação e então estendeu com configurações.  
  
 Quando os pacotes são executados, cada executável do pacote fica com uma cor verde quando concluído com sucesso. Quando todos os executáveis estão verdes, o pacote foi concluído com sucesso. Você também pode visualizar o progresso da execução do pacote na guia **Progresso** .  
  
 Se os pacotes não forem executados com sucesso, você precisará corrigi-los antes de ir para a próxima lição.  
  
### <a name="to-run-the-datatransfer-package"></a>Para executar o pacote DataTransfer  
  
1.  No Gerenciador de Soluções, clique em DataTransfer.dtsx.  
  
2.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
### <a name="to-run-the-loadxmldata-package"></a>Para executar o pacote LoadXMLData  
  
1.  No Gerenciador de Soluções, clique em LoadXMLData.dtsx.  
  
2.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Criando o pacote de implantação](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
![Ícone do Integration Services (pequeno)](media/dts-16.gif "ícone do Integration Services (pequeno)")**permanecer acima para data com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  