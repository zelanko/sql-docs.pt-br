---
title: Exportar informações de servidor registrado (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.exportregisteredservers.f1
helpviewer_keywords:
- Registered Servers [SQL Server], exporting
- exporting registered server information
- transferring registered server information
ms.assetid: b65e168f-b6bf-489c-b8ad-3b8644acf0b6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9d1a853c5469fc30ef9545c0a062fdd1933f5c9b
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65104407"
---
# <a name="export-registered-server-information-sql-server-management-studio"></a>Exportar informações de servidor registrado (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Este tópico descreve como salvar e exportar informações de servidor registrado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]e distribuí-las para outros empregados ou servidores. É possível usar esse recurso de exportação para apresentar uma interface com o usuário consistente em computadores múltiplos.  
  
 Exportar e, depois, importar os arquivos de Servidores Registrados permite que você configure facilmente vários computadores com os mesmos servidores em Servidores Registrados. Isso é útil quando se gerencia um grande número de servidores de computadores em diversos locais ou quando você deseja configurar um usuário menos experiente com configurações de conexão básica.  
  
> [!NOTE]  
>  Os registros de servidores que usam a autenticação do SQL Server armazenam senhas por usuário. Depois de exportar e importar os registros de servidores, os usuários devem digitar a senha para cada servidor quando se conectarem pela primeira vez, armazenando as senhas em suas listas de servidores registrados. Isso não é necessário para servidores registrados que usam a autenticação do Windows.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-export-registered-server-information"></a>Para exportar informações de servidor registrado  
  
1.  Em Servidores Registrados, clique com o botão direito do mouse em um grupo de servidores e clique em **Exportar**.  
  
    > [!NOTE]  
    >  Você pode exportar um servidor individual, toda a árvore de servidores registrados ou um subconjunto da árvore de servidores registrados.  
  
2.  Na caixa de diálogo **Exportar Servidores Registrados** , faça as seguintes seleções:  
  
     **Grupo de servidor**  
     Especifique o grupo de servidor que será exportado. Exporte todos os servidores registrados, servidores registrados em um grupo de servidores específicos ou um único servidor registrado para o arquivo de exportação. A funcionalidade de exportação é recursiva; por exemplo, se o grupo de servidores A contiver o grupo de servidores B, e o grupo de servidores B contiver os grupos de servidores C e D, a exportação do grupo de servidores A exportará todas as entradas em A, B, C e D.  
  
     O grupo de servidores exibe somente os grupos da árvore atual de servidores registrados.  
  
     **Arquivo de exportação**  
     Digite o nome do arquivo de exportação na caixa de texto ou use o botão Procurar (**...**) para localizar um arquivo de exportação no computador cliente. Se você selecionar um arquivo existente, a informação de servidor registrado será anexada ao arquivo. Use a extensão .regsrvr. Se você quiser que as informações do servidor registrado estejam disponíveis para outros usuários ou outro computador, você poderá salvar o arquivo na rede. Outros usuários podem acessar o arquivo e podem importar parte ou todas as informações do servidor registrado. Se você selecionar um arquivo existente como o arquivo de exportação, o conteúdo do arquivo será substituído pelas informações de registro do servidor.  
  
     **Não inclua nomes de usuário e senhas no arquivo de exportação**  
     Exclua nomes de usuário ao exportar o arquivo.  
  
    > [!IMPORTANT]  
    >  Embora os arquivos de exportação sejam criptografados, se nomes de usuários e senhas da autenticação do SQL Server forem incluídas no arquivo, o acesso ao arquivo deve ser cuidadosamente controlado. Portanto, os nomes de usuários e senhas são excluídos do arquivo de exportação por padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Importar informações de servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)   
 [Criar um novo servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)  
  
  
