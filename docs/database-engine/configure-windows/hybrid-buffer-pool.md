---
title: Pool de buffers híbrido | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.openlocfilehash: a8098c38b72ba44ab973fe5564b93740252bafc6
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560303"
---
# <a name="hybrid-buffer-pool"></a>Pool de Buffers Híbrido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Com o SQL Server de 2019 CTP 2.1, um novo recurso é introduzido no mecanismo de banco de dados do SQL Server que permite que ele acesse diretamente as páginas de dados em arquivos de banco de dados armazenados em dispositivos de memória persistente (PMEM). 

Em um sistema tradicional sem memória persistente, o SQL Server armazenará em cache páginas de dados no pool de buffers. Com o Pool de Buffers Híbrido, o SQL Server ignora a execução de uma cópia da página para a parte do pool de buffers baseada em DRAM e, em vez disso, faz referência à página diretamente no arquivo de banco de dados que reside em um dispositivo PMEM. O acesso a arquivos de dados no PMEM para o Pool de Buffers Híbrido é realizado usando E/S mapeado em memória, também conhecido como esclarecimento.

Somente páginas limpas podem ser referenciadas diretamente em um dispositivo PMEM. Quando uma página se tornar suja, ela será mantida na DRAM e eventualmente será gravada de volta no dispositivo PMEM.

Esse recurso está disponível no Windows e no Linux.

## <a name="enable-hybrid-buffer-pool"></a>Habilitar pool de buffers híbrido

No CTP 2.1, você deve habilitar o sinalizador de rastreamento de inicialização 809 para usar o Pool de Buffers Híbrido.

## <a name="best-practices-for-hybrid-buffer-pool"></a>Práticas recomendadas para o Pool de Buffers Híbrido

* Ao formatar seu dispositivo PMEM no Windows, use o maior tamanho de unidade de alocação disponível para NTFS (2 MB no Windows Server 2019) e verifique se o dispositivo foi habilitado para DAX (DirectAccess)
  