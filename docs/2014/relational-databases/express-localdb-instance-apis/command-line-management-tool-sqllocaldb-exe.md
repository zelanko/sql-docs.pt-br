---
title: 'Ferramenta de gerenciamento de linha de comando: SqlLocalDB. exe | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 58ea983555fdcb4bb177813db88d40f4bcc59c0e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63128780"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Ferramenta de gerenciamento da linha de comando: SqlLocalDB.exe
  O SqlLocalDB.exe é uma ferramenta simples que permite ao usuário a gerenciar facilmente as instâncias de LocalDB na linha de comando. É implementado como um wrapper simples com base na instância da API de LocalDB. Assim como ocorre em muitas ferramentas semelhantes do SQL Server (por exemplo, SQLCMD), os parâmetros são passados para SqlLocalDB como argumentos de linha de comando e a saída é enviada ao console.  
  
 O SqlLocalDB permite que os desenvolvedores utilizem o LocalDB sem precisar escrever o código para chamar a API ou depender de outras ferramentas para fazer isso para eles.  
  
## <a name="sqllocaldb-options"></a>Opções de SqlLocalDB  
 O SqlLocalDB oferece suporte para as seguintes opções.  
  
|Opção|O que faz|  
|------------|------------------|  
|`-?`|Imprime o texto da Ajuda.|  
|`create&#124;c "instance name" [version-number] [-s]`|Cria uma nova instância de LocalDB com um nome e uma versão especificados.<br /><br /> Se o parâmetro [version-number] for omitido, o valor padrão será a versão de compilação do SqlLocalDB.<br /><br /> - s inicia a nova instância de LocalDB depois que ela é criada.|  
|`delete&#124;d "instance name"`|Excluir a instância de LocalDB com o nome especificado.|  
|`start&#124;s "instance name"`|Inicia a instância de LocalDB com o nome especificado.|  
|`stop&#124;p "instance name" [-i&#124;-k]`|Interrompe a instância de LocalDB com o nome especificado, depois que a execução das consultas atuais são concluídas.<br /><br /> -i solicita o desligamento da instância de LocalDB com a opção NOWAIT.<br /><br /> -k elimina o processo da instância de LocalDB sem contatá-la.|  
|`share&#124;h ["owner SID or account"] "private name" "shared name"`|Compartilha a instância privada especificada que usa o nome compartilhado especificado. Se a SID ou o nome de conta do usuário for omitido, o valor padrão será o usuário atual.|  
|`unshare&#124;u "shared name"`|Descompartilha a instância de LocalDB especificada.|  
|`info&#124;i`|Lista todas as instâncias de LocalDB existentes pertencentes ao usuário atual e todas as instâncias de LocalDB compartilhadas.|  
|`info&#124;i "instance name"`|Imprime as informações sobre a instância de LocalDB especificada.|  
|`versions&#124;v`|Lista todas as versões de LocalDB instaladas no computador.|  
|||  
|`trace&#124;t on&#124;off`|Ativa e desativa o rastreamento.|  
  
 O SqlLocalDB trata os espaços como delimitadores; você deve delimitar os nomes de instância que contêm espaços e caracteres especiais com aspas. Por exemplo:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
