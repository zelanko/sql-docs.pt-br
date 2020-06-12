---
title: Anexar e desanexar bancos de dados Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.detachdatabase.f1
- sql12.asvs.ssms.attachdatabase.f1
- sql12.asvs.ssmsimbi.AttachDatabase.f1
- sql12.asvs.ssmsimbi.DetachDatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
author: minewiskan
ms.author: owend
ms.openlocfilehash: a0c62698f1aed231128803cb91c80264a2fbdbf4
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544828"
---
# <a name="attach-and-detach-analysis-services-databases"></a>Anexar e desanexar Bancos de Dados do Analysis Services
  Existem situações frequentes em que um DBA (administrador de banco de dados) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deseja colocar o banco de dados offline em determinado período e colocá-lo online novamente na mesma instância do servidor ou em uma instância diferente. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como a movimentação do banco de dados para um disco diferente em busca de um melhor desempenho, a obtenção de espaço para o crescimento do banco de dados ou para a atualização de um produto. Para todos esses casos e muito mais, `Attach` os `Detach` comandos e permitem que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA Coloque o banco de dados offline e coloque-o online novamente com pouco esforço.  
  
## <a name="attach-and-detach-commands"></a>Comandos Anexar e Desanexar  
 O comando `Attach` permite que o banco de dados que estava offline seja alterado para online. Você pode anexar o banco de dados à instância do servidor original ou a outra instância. Ao anexar um banco de dados, o usuário pode especificar a configuração **ReadWriteMode** para o banco de dados. O comando `Detach` permite colocar no modo offline um banco de dados do servidor.  
  
## <a name="attach-and-detach-usage"></a>Uso dos comandos Anexar e Desanexar  
 O comando `Attach` é usado para colocar uma estrutura de banco de dados existente no modo online. Caso o banco de dados esteja anexado em modo `ReadWrite`, ele poderá ser anexado somente uma vez em uma instância de servidor. No entanto, caso o banco de dados esteja anexado em modo `ReadOnly`, ele poderá ser anexado várias vezes em diferentes instâncias de servidor. O mesmo banco de dados não pode ser anexado mais de uma vez à mesma instância de servidor. Ocorrerá um erro se você tentar anexar o mesmo banco de dados mais de uma vez, mesmo se os dados forem copiados para pastas diferentes.  
  
> [!IMPORTANT]  
>  Se for preciso informar uma senha para desanexar o banco de dados, a mesma senha será necessária para anexar o banco de dados.  
  
 O comando `Detach` é usado para colocar uma estrutura de banco de dados existente no modo offline. Ao desanexar o banco de dados, é preciso fornecer uma senha para proteger os metadados confidenciais.  
  
> [!IMPORTANT]  
>  Para proteger o conteúdo dos arquivos de dados, use uma lista de controle de acesso para a pasta, as subpastas e os arquivos de dados.  
  
 Ao desanexar um banco de dados, o servidor segue estas etapas.  
  
|Desanexar um banco de dados de leitura/gravação|Desanexar um banco de dados somente leitura|  
|--------------------------------------|-------------------------------------|  
|1) O servidor emite uma solicitação para um Bloqueio de CommitExclusive no banco de dados<br />2) O servidor espera até que todas as transações contínuas sejam confirmadas ou revertidas<br />3) O servidor cria todos os metadados necessários para desanexar o banco de dados<br />4) O banco de dados é marcado como excluído<br />5) O servidor confirma a transação|1) O banco de dados é marcado como excluído<br />2) O servidor confirma a transação<br /><br /> <br /><br /> Observação: a senha para desanexar não pode ser alterada para um banco de dados somente leitura. Ocorrerá um erro caso o parâmetro de senha seja fornecido a um banco de dados anexado que já tenha uma senha.|  
  
 Os comandos `Attach` e `Detach` devem ser executados como operações únicas. Eles não podem ser combinados com outras operações na mesma transação. Além disso, `Attach` os `Detach` comandos e são comandos transacionais atômicos. Isso significa que a operação poderá ser bem-sucedida ou não. Nenhum banco de dados ficará incompleto.  
  
> [!IMPORTANT]  
>  Para executar o comando `Detach`, é preciso ter privilégios de administrador do banco de dados ou do servidor.  
  
> [!IMPORTANT]  
>  Para executar o comando `Attach`, é preciso ter privilégios de administrador do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Mover um banco de dados Analysis Services](move-an-analysis-services-database.md)   
 [ReadWriteModes do banco de dados](database-readwritemodes.md)   
 [Alternar um banco de dados Analysis Services entre os modos ReadOnly e ReadWrite](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Elemento Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  
