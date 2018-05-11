---
title: Anexar e desanexar bancos de dados do Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55d490d5fa8ca9dadeacdf9b5fd9e77c3edcb057
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="attach-and-detach-analysis-services-databases"></a>Anexar e desanexar Bancos de Dados do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Existem situações frequentes em que um DBA (administrador de banco de dados) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deseja colocar o banco de dados offline em determinado período e colocá-lo online novamente na mesma instância do servidor ou em uma instância diferente. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como a movimentação do banco de dados para um disco diferente em busca de um melhor desempenho, a obtenção de espaço para o crescimento do banco de dados ou para a atualização de um produto. Para todos estes e outros casos, os comandos **Attach** e **Detach** permitem que o DBA do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] coloque o banco de dados offline e o coloque online novamente com o mínimo de esforço.  
  
## <a name="attach-and-detach-commands"></a>Comandos Anexar e Desanexar  
 O comando **Attach** permite que o banco de dados que estava offline seja alterado para online. Você pode anexar o banco de dados à instância do servidor original ou a outra instância. Ao anexar um banco de dados, o usuário pode especificar a configuração **ReadWriteMode** para o banco de dados. O comando **Detach** permite colocar no modo offline um banco de dados do servidor.  
  
## <a name="attach-and-detach-usage"></a>Uso dos comandos Anexar e Desanexar  
 O comando **Attach** é usado para colocar uma estrutura de banco de dados existente no modo online. Caso o banco de dados esteja anexado em modo **ReadWrite** , ele poderá ser anexado somente uma vez em uma instância de servidor. No entanto, caso o banco de dados esteja anexado em modo **ReadOnly** , ele poderá ser anexado várias vezes em diferentes instâncias de servidor. O mesmo banco de dados não pode ser anexado mais de uma vez à mesma instância de servidor. Ocorrerá um erro se você tentar anexar o mesmo banco de dados mais de uma vez, mesmo se os dados forem copiados para pastas diferentes.  
  
> [!IMPORTANT]  
>  Se for preciso informar uma senha para desanexar o banco de dados, a mesma senha será necessária para anexar o banco de dados.  
  
 O comando **Detach** é usado para colocar uma estrutura de banco de dados existente no modo offline. Ao desanexar o banco de dados, é preciso fornecer uma senha para proteger os metadados confidenciais.  
  
> [!IMPORTANT]  
>  Para proteger o conteúdo dos arquivos de dados, use uma lista de controle de acesso para a pasta, as subpastas e os arquivos de dados.  
  
 Ao desanexar um banco de dados, o servidor segue estas etapas.  
  
|Desanexar um banco de dados de leitura/gravação|Desanexar um banco de dados somente leitura|  
|--------------------------------------|-------------------------------------|  
|1) O servidor emite uma solicitação para um Bloqueio de CommitExclusive no banco de dados<br /><br /> 2) O servidor espera até que todas as transações contínuas sejam confirmadas ou revertidas<br /><br /> 3) O servidor cria todos os metadados necessários para desanexar o banco de dados<br /><br /> 4) O banco de dados é marcado como excluído<br /><br /> 5) O servidor confirma a transação|1) O banco de dados é marcado como excluído<br /><br /> 2) O servidor confirma a transação<br /><br /> Observação: a senha para desanexar não pode ser alterada para um banco de dados somente leitura. Ocorrerá um erro caso o parâmetro de senha seja fornecido a um banco de dados anexado que já tenha uma senha.|  
  
 Os comandos **Attach** e **Detach** devem ser executados como operações únicas. Eles não podem ser combinados com outras operações na mesma transação. Os comandos **Attach** e **Detach** também são comandos transacionais atômicos. Isso significa que a operação poderá ser bem-sucedida ou não. Nenhum banco de dados ficará incompleto.  
  
> [!IMPORTANT]  
>  É preciso ter privilégios de administrador do banco de dados ou do servidor para executar o comando **Detach** .  
  
> [!IMPORTANT]  
>  É preciso ter privilégios de administrador do servidor para executar o comando **Attach** .  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Mover um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Banco de dados ReadWriteModes](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Elemento Detach](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Elemento Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  
