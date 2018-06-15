---
title: Depuração de procedimentos armazenados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d37eebfad3f8a3e89dc65ad9602f4b5d61b5072e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024983"
---
# <a name="debugging-stored-procedures"></a>Depurando procedimentos armazenados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Os procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são, na verdade, bibliotecas CLR ou COM (normalmente DLLs) escritas em C# (ou em outra linguagem CLR ou COM). Portanto, depurar um procedimento armazenado é bem parecido com depurar outro aplicativo no ambiente de depuração do Visual Studio. Você depura procedimentos armazenados no ambiente de desenvolvimento do Visual Studio usando funções de depuração integradas. Elas permitem que você pare nas localizações do procedimento, verifique a memória e os valores do Registro, altere variáveis, observe o tráfego de mensagens e analise como o código funciona.  
  
### <a name="to-debug-a-stored-procedure"></a>Depurar um procedimento armazenado  
  
1.  Abra o projeto usado para criar a DLL no Visual Studio.  
  
2.  Crie pontos de interrupção no método ou na função correspondente ao procedimento que você deseja depurar.  
  
3.  Use o Visual Studio para criar uma compilação para depuração de uma DLL de procedimentos armazenados.  
  
4.  Implante a DLL no servidor. Para obter mais informações sobre como implantar a DLL para o servidor, consulte [Criando procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md).  
  
5.  Você precisa de um aplicativo que chame o procedimento armazenado que deseja testar. Se ainda não houver um aplicativo pronto, use o Editor de Consultas MDX do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar uma consulta MDX para chamar o procedimento armazenado que será testado.  
  
6.  No Visual Studio, anexe ao processo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (Msmdsrv.exe).  
  
    1.  Do **depurar** menu, escolha **toProcess anexar**.  
  
    2.  No **anexar toProcess** caixa de diálogo, selecione **Mostrar processos de todos os usuários**.  
  
    3.  No **processos disponíveis** lista, o **processo** coluna, clique em **Msmdsrv.exe**. Se houver mais que uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em execução no servidor, será necessário identificar o processo pelo ID da instância que você deseja usar.  
  
    4.  No **anexar a** texto caixa, certifique-se de que o tipo de programa apropriado está selecionado. Para uma DLL CLR, clique em **selecione**, em seguida, clique em **depurar esses tipos de código**, em seguida, clique em **gerenciado**, em seguida, clique em **Okey**. Para uma DLL COM, clique em **selecione**, em seguida, clique em **depurar esses tipos de código**, em seguida, clique em **nativo**, em seguida, clique em **Okey**.  
  
    5.  Clique em **anexar**.  
  
7.  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], acione o programa ou script MDX que chama o procedimento armazenado. O depurador será interrompido quando chegar a uma linha que contém um ponto de interrupção. Você pode avaliar variáveis na janela de informação, exibir os locais e navegar pelo código.  
  
 Se houver problemas ao depurar uma biblioteca, certifique-se de que o arquivo do banco de dados do programa correspondente (arquivo PDB) foi copiado para o local de implantação no servidor. Se esse arquivo não foi copiado durante o registro ou a implantação, copie-o manualmente no mesmo local onde está a DLL. No caso de código nativo (DLL COM), o arquivo PDB reside no subdiretório \debug. Para código gerenciado (DLL CLR), reside no subdiretório \WINDEBUG.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Assemblies de modelo multidimensional](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
