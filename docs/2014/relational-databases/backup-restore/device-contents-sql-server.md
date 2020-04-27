---
title: Conteúdos do dispositivo (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.bnrdevicecontents.f1
ms.assetid: 95e1902e-8c7a-4830-bdf9-1a6aca414a24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 890a03221888693c1696059ed5d31a9907ea2872
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62876017"
---
# <a name="device-contents-sql-server"></a>Conteúdos do dispositivo (SQL Server)
  Use essa caixa de diálogo para exibir informações de backup. As informações descrevem o dispositivo, a mídia, o conjunto de mídias e o conjunto ou conjuntos de backups.  
  
 **Para usar o SQL Server Management Studio para exibir o conteúdo de um dispositivo de backup**  
  
-   [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opções  
 **Mídia**  
 Um disco ou um conjunto de fitas nos quais as informações de backup estão armazenadas.  
  
 **Sequência de mídia**  
 Relaciona o número de sequência de mídia; o número de sequência familiar e o identificador de espelhos, se houver. Todas as mídias físicas de backup são marcadas com o número de sequência da mídia que indica a ordem de utilização da mídia. A primeira mídia do backup é marcada com 1; a segunda (primeira fita de continuação) é marcada com 2, e assim sucessivamente. Quando o conjunto de backups for restaurado, os números da sequência de mídias assegurarão que o operador que restaure o backup monte as mídias corretas na ordem correta.  
  
 **Criado em**  
 Exibe a data da mídia.  
  
 **Conjunto de mídias**  
 Um conjunto de mídias é uma coleção ordenada de mídias de backup em que uma ou mais operações de backup foram gravadas, usando um número constante de dispositivos de backup.  
  
 **Nome**  
 Exibe o nome do conjunto de mídias.  
  
 **Descrição**  
 Exibe o conjunto de mídias de descrição.  
  
 **Contagem de família de mídia**  
 Exibe a conta de família de mídia. Cada conjunto de mídias é uma coleção de uma ou mais famílias de mídias. Toda a saída de um determinado dispositivo de backup único (ou grupo de dispositivos de backup espelhados) forma uma única família de mídias. Cada conjunto de mídias contém uma família para cada dispositivo separado (ou grupo de dispositivos espelhados); por exemplo, se um conjunto de mídias utiliza dois dispositivos de backup não espelhados, o mesmo terá duas famílias de mídias.  
  
 **Conjuntos de backup**  
 Exibe as informações sobre o conjunto ou conjuntos de backup incluídos na mídia. Um conjunto de backup é o resultado de uma operação de backup bem-sucedida, cujo conteúdo é distribuído entre as mídias em um conjunto de dispositivos de backup.  
  
|Cabeçalho|Valores|  
|------------|------------|  
|**Nome**|O nome do conjunto de backup.|  
|**Tipo**|O tipo de backup efetuado: Completo, Diferencial ou Log de Transações.|  
|**Componente**|O componente com backup: Banco de Dados, Arquivo ou *\<blank>* (para logs de transações).|  
|**Servidor**|O nome da instância de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que realizou a operação de backup.|  
|**Backup de banco de dados**|O nome do banco de dados cujo backup foi efetuado.|  
|**Posição**|A posição do conjunto de backup no volume.|  
|**Data**|A data e hora da conclusão da operação de backup, apresentadas na configuração regional do cliente.|  
|**Tamanho**|O tamanho do conjunto de backup em bytes.|  
|**Nome de usuário**|O nome do usuário que realizou a operação de backup.|  
|**Validade**|A data e hora de validade do conjunto de backup.|  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
