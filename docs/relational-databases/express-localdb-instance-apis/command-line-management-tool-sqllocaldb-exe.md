---
title: 'Ferramenta de gerenciamento de linha de comando: SqlLocalDB.exe | Microsoft Docs'
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apilocation: sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6ffc8033651fedbe906086f0a35ef31d463f6e31
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Ferramenta de gerenciamento da linha de comando: SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]O SqlLocalDB.exe é uma ferramenta simples que permite que o usuário gerencie facilmente as instâncias de LocalDB na linha de comando. É implementado como um wrapper simples com base na instância da API de LocalDB. Assim como ocorre em muitas ferramentas semelhantes do SQL Server (por exemplo, SQLCMD), os parâmetros são passados para SqlLocalDB como argumentos de linha de comando e a saída é enviada ao console.  
  
 O SqlLocalDB permite que os desenvolvedores utilizem o LocalDB sem precisar escrever o código para chamar a API ou depender de outras ferramentas para fazer isso para eles.  
  
## <a name="sqllocaldb-options"></a>Opções de SqlLocalDB  
 O SqlLocalDB oferece suporte para as seguintes opções.  
  
|Opção|O que ele faz|  
|------------|------------------|  
|`-?`|Imprime o texto da Ajuda.|  
|' create\|c "nome da instância" [número de versão] [-s]'|Cria uma nova instância de LocalDB com um nome e uma versão especificados.<br /><br /> Se o parâmetro [version-number] for omitido, o valor padrão será a versão de compilação do SqlLocalDB.<br /><br /> - s inicia a nova instância de LocalDB depois que ela é criada.|  
|' delete\|d "nome da instância" '|Excluir a instância de LocalDB com o nome especificado.|  
|' Start|s "nome da instância" '|Inicia a instância de LocalDB com o nome especificado.|  
|' Stop|p "nome da instância" [-i\|-k]'|Interrompe a instância de LocalDB com o nome especificado, depois que a execução das consultas atuais são concluídas.<br /><br /> -i solicita o desligamento da instância de LocalDB com a opção NOWAIT.<br /><br /> -k elimina o processo da instância de LocalDB sem contatá-la.|  
|' share\|h ["SID do proprietário ou conta"] "nome particular" "nome compartilhado" '|Compartilha a instância privada especificada que usa o nome compartilhado especificado. Se a SID ou o nome de conta do usuário for omitido, o valor padrão será o usuário atual.|  
|' unshare\|u "nome compartilhado" '|Descompartilha a instância de LocalDB especificada.|  
|' info\|i'|Lista todas as instâncias de LocalDB existentes pertencentes ao usuário atual e todas as instâncias de LocalDB compartilhadas.|  
|' info\|i "nome da instância" '|Imprime as informações sobre a instância de LocalDB especificada.|  
|' versions\|v'|Lista todas as versões de LocalDB instaladas no computador.|  
|||  
|' trace\|t on\|Desativar '|Ativa e desativa o rastreamento.|  
  
 O SqlLocalDB trata os espaços como delimitadores; você deve delimitar os nomes de instância que contêm espaços e caracteres especiais com aspas. Por exemplo:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
