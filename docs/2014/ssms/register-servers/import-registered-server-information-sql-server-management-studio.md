---
title: Importar informações de servidor registrado (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.importregisteredservers.f1
helpviewer_keywords:
- transferring registered server information
- Registered Servers [SQL Server], importing
- importing registered server information
ms.assetid: cc497a14-1360-4887-b70c-002f042823b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0106bc32724bbe4e2e2faed4ead5750440508d7d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191889"
---
# <a name="import-registered-server-information-sql-server-management-studio"></a>Importar informações de servidor registrado (SQL Server Management Studio)
  Este tópico descreve como importar informações do servidor registrado salvas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Ao exportar e, em seguida, importar os arquivos de servidores registrados, você poderá facilmente configurar vários computadores com os mesmos servidores em Servidores Registrados. Isso é útil ao gerenciar um grande número de servidores de computadores em diversos locais ou quando você deseja definir configurações de conexão básica para um usuário menos experiente.  
  
> [!NOTE]  
>  Você não pode importar informações do servidor registradas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de versões anteriores ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-import-registered-server-information"></a>Para importar informações de servidor registrado  
  
1.  Em Servidores Registrados, clique em tipo de servidor na barra de ferramentas Servidores Registrados. O tipo de servidor deve ser igual ao tipo de arquivo de exportação do servidor registrado. Por exemplo, se você exportou informações do servidor registrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , deverá clicar em **SQL Server** na barra de ferramentas Servidores Registrados.  
  
2.  Clique com o botão direito do mouse em um grupo de servidores e selecione **Importar**.  
  
3.  Na caixa de diálogo **Importar Servidores Registrados** , selecione os arquivos de servidores registrados a serem importados e clique em **OK**.  
  
     **Arquivo de importação**  
     Digite o nome do arquivo de importação na caixa de texto ou clique no botão Procurar (**...**) para localizar o arquivo de importação no computador cliente. Se você selecionar um arquivo existente, a informação de servidor registrado será anexada ao arquivo. O arquivo de importação só pode ser um arquivo de servidor registrado exportado anteriormente. Os arquivos de servidor registrado têm uma extensão .regsrvr.  
  
     **Selecione o grupo de servidores para o qual importar**  
     Selecione o nó raiz ou um grupo de servidores específico para o qual serão importadas as entradas do servidor registrado no arquivo. Você pode importar todos os servidores registrados, servidores registrados em um grupo de servidores específico ou um único servidor registrado para o arquivo de exportação. A funcionalidade de importação é recursiva; por exemplo, se o grupo de servidores A contiver o grupo de servidores B e o grupo de servidores B contiver os grupos de servidores C e D, a importação do grupo de servidores A exportará todas as entradas em A, B, C e D.  
  
     O grupo de servidores exibe somente os grupos da árvore atual de servidores registrados.  
  
     Se você selecionar importar um grupo de servidores ou um servidor existente, uma mensagem confirmará que você deseja substituir o servidor ou o grupo de servidores existente.  
  
 Os registros de servidores que usam a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenam senhas por usuário. Depois de importar os registros de servidores, os usuários devem digitar a senha para cada servidor quando se conectarem pela primeira vez, armazenando as senhas em suas listas de servidores registrados. Isso não é necessário para servidores registrados por meio da autenticação do Windows.  
  
## <a name="see-also"></a>Consulte também  
 [Alterar um registro do servidor &#40;SQL Server Management Studio&#41; ](change-a-server-s-registration-sql-server-management-studio.md) [exportar informações de servidor registrado &#40;SQL Server Management Studio&#41;](export-registered-server-information-sql-server-management-studio.md)   
 [Criar um novo servidor registrado &#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md)  
  
  
