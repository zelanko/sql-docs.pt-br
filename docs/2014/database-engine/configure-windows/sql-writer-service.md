---
title: Serviço Gravador do SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- VDI [SQL Server]
- restoring [SQL Server], SQL Writer Service
- backups [SQL Server], while SQL Server running
- Volume Shadow Copy Service
- volume backups while running [SQL Server]
- Virtual Backup Device Interface [SQL Server]
- SQL Writer Service
- services [SQL Server], SQL Writer
- MSDE Writer
- VSS
ms.assetid: 0f299867-f499-4c2a-ad6f-b2ef1869381d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7204d2f20c7c299a2bcefcc66409182c8846affc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62755439"
---
# <a name="sql-writer-service"></a>Serviço do gravador do SQL
  O Serviço Gravador do SQL oferece funcionalidade adicional para fazer backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio da estrutura do Serviço de Cópias de Sombra de Volume.  
  
 O Serviço Gravador do SQL é instalado automaticamente. Deve estar em execução quando o aplicativo VSS (Volume Shadow Copy Service) pedir um backup ou uma restauração. Para configurar o serviço, use o miniaplicativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] do Windows Services. O Serviço Gravador do SQL é instalado em todos os sistemas operacionais.  
  
## <a name="purpose"></a>Finalidade  
 Quando está em execução, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] bloqueia os arquivos de dados e tem acesso exclusivo a eles. Quando o Serviço Gravador do SQL não está em execução, os programas de backup em execução no Windows não têm acesso aos arquivos de dados e os backups devem ser executados usando o backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Use o Serviço Gravador do SQL para permitir que os programas de backup do Windows copiem arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver executando.  
  
## <a name="volume-shadow-copy-service"></a>Serviço de cópias de sombra de volume  
 O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir que backups dos volumes sejam feitos enquanto os aplicativos em um sistema continuam a gravar nos volumes. O VSS oferece uma interface consistente que permite a coordenação entre os aplicativos de usuário que atualizam dados em disco (gravadores) e os aplicativos de backup (solicitantes).  
  
 O VSS captura e copia imagens estáveis para backup em sistemas em execução, particularmente servidores, sem degradar indevidamente o desempenho e a estabilidade dos serviços que oferecem. Para obter mais informações sobre o VSS, consulte sua documentação do Windows.  
  
## <a name="virtual-backup-device-interface-vdi"></a>VDI (Virtual Backup Device Interface)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece uma API chamada VDI que permite que fornecedores de software independente integrem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seus produtos para dar suporte a operações de backup e restauração. Essas APIs são criadas para prover confiabilidade e desempenho máximos, e dão suporte a todas as funcionalidades de backup e de restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , inclusive todas as capacidades de backup hot e instantâneo.  
  
## <a name="permissions"></a>Permissões  
 O Serviço Gravador do SQL deve ser executado na conta **Sistema Local** . O Serviço Gravador do SQL usa o logon **NT Service\SQLWriter** para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O uso do logon **NT Service\SQLWriter** permite que o processo do Gravador do SQL seja executado no nível mais baixo de privilégio em uma conta designada como **nenhum logon**, que limita a vulnerabilidade. Se o serviço do Gravador do SQL estiver desabilitado, qualquer utilitário que confie em instantâneos do VSS, como o System Center Data Protection Manager, bem como em outros produtos de terceiros, será interrompido, ou pior, correrá o risco de obter backups de bancos de dados que não estavam consistentes. Se nem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o sistema em que é executado, nem o sistema host (no caso de uma máquina virtual), precisarem usar qualquer coisa além do backup de [!INCLUDE[tsql](../../includes/tsql-md.md)] , o serviço do Gravador do SQL poderá seguramente ser desabilitado e o logon será removido.  Observe que o serviço do Gravador do SQL pode ser chamado por um backup em nível de sistema ou de volume, seja o backup diretamente baseado em instantâneo ou não. Alguns produtos de backup de sistema usam o VSS para evitar serem bloqueados por arquivos abertos ou bloqueados. O Serviço Gravador do SQL precisa de permissões elevadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pois, no decorrer de suas atividades, ele congelará brevemente qualquer E/S para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="features"></a>Recursos  
 O Gravador do SQL dá suporte a:  
  
-   Backup e restauração de banco de dados completos inclusive catálogos de texto completo  
  
-   Backup diferencial e restauração  
  
-   Restaurar e mover  
  
-   Renomear banco de dados  
  
-   Backup somente cópia  
  
-   Recuperação automática de instantâneo do banco de dados  
  
 O Gravador do SQL não dá suporte a:  
  
-   Backups de log  
  
-   Backup de arquivo e grupo de arquivos  
  
-   Restauração de página  
  
  
