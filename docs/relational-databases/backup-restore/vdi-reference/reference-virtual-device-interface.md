---
title: Referência da interface de dispositivo virtual
titlesuffix: SQL Server VDI reference
description: Este artigo fornece uma visão geral da referência da interface de dispositivo virtual para o backup do SQL Server.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2b4556734044ad5bd688f8d5b286885450897b42
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847147"
---
# <a name="virtual-device-interface-vdi-reference"></a>Referência da VDI (interface de dispositivo virtual)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta seção contém as especificações para interfaces de programação de aplicativo do SQL Server destinadas a serem usadas por fornecedores de software de backup de terceiros.

## <a name="overview"></a>Visão geral

A VDI (interface de dispositivo virtual) fornece a taxa de transferência de backup online mais alta com degradação mínima para a carga de trabalho da transação, bem como os tempos de restauração mais rápidos possíveis. Ela permite que os fornecedores de terceiros obtenham as mesmas características de desempenho de backup/restauração nativos do SQL Server, além de disponibilizar toda a gama de funcionalidades de backup/restauração. A VDI foi introduzida no SQL Server 7.0 e é compatível com versões posteriores, tendo sido aprimorada nelas.

A VDI dá suporte a dois tipos principais de tecnologias de backup:

- Backups online convencionais, em que todo o conteúdo do conjunto de backup é lido e transferido para a mídia de backup.

- Backups de instantâneos usando a tecnologia subjacente de espelho dividido ou cópia em gravação.

Os backups online convencionais feitos por meio da VDI podem aproveitar toda a gama de recursos de backup e restauração no SQL Server. Os backups de instantâneos são limitados somente a backups completos de banco de dados e de arquivo/grupo de arquivos. No entanto, os backups de instantâneos podem ter roll forward com backups de log de transações, diferenciais de arquivo e diferenciais de banco de dados convencionais.

## <a name="next-steps"></a>Próximas etapas

Examine a documentação de referência da VDI nesta seção.

Baixe a especificação completa e os arquivos de origem de suporte:

[Especificação da VDI (interface de dispositivo de backup virtual) do SQL Server 2005](https://www.microsoft.com/download/details.aspx?id=17282)