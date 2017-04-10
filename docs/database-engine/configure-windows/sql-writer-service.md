---
title: "Servi&#231;o do gravador do SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "VDI [SQL Server]"
  - "restaurando [SQL Server], Serviço Gravador do SQL"
  - "backups [SQL Server], durante a execução do SQL Server"
  - "Serviço de cópias de sombra de volume"
  - "backups de volume durante execução [SQL Server]"
  - "Interface de dispositivo de backup virtual [SQL Server]"
  - "Serviço do gravador do SQL"
  - "serviços [SQL Server], Gravador do SQL"
  - "Gravador MSDE"
  - "VSS"
ms.assetid: 0f299867-f499-4c2a-ad6f-b2ef1869381d
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Servi&#231;o do gravador do SQL
  O Serviço Gravador do SQL oferece funcionalidade adicional para fazer backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio da estrutura do Serviço de Cópias de Sombra de Volume.  
  
 O Serviço Gravador do SQL é instalado automaticamente. Deve estar em execução quando o aplicativo VSS (Volume Shadow Copy Service) pedir um backup ou uma restauração. Para configurar o serviço, use o miniaplicativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] do Windows Services. O Serviço Gravador do SQL é instalado em todos os sistemas operacionais.  
  
## Finalidade  
 Quando está em execução, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] bloqueia os arquivos de dados e tem acesso exclusivo a eles. Quando o Serviço Gravador do SQL não está em execução, os programas de backup em execução no Windows não têm acesso aos arquivos de dados e os backups devem ser executados usando o backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Use o Serviço Gravador do SQL para permitir que os programas de backup do Windows copiem arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver executando.  
  
## Serviço de cópias de sombra de volume  
 O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir que backups dos volumes sejam feitos enquanto os aplicativos em um sistema continuam a gravar nos volumes. O VSS oferece uma interface consistente que permite a coordenação entre os aplicativos de usuário que atualizam dados em disco (gravadores) e os aplicativos de backup (solicitantes).  
  
 O VSS captura e copia imagens estáveis para backup em sistemas em execução, particularmente servidores, sem degradar indevidamente o desempenho e a estabilidade dos serviços que oferecem. Para obter mais informações sobre o VSS, consulte sua documentação do Windows.  
  
## VDI (Virtual Backup Device Interface)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece uma API chamada VDI que permite que fornecedores de software independente integrem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seus produtos para dar suporte a operações de backup e restauração. Essas APIs são criadas para prover confiabilidade e desempenho máximos, e dão suporte a todas as funcionalidades de backup e de restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], inclusive todas as capacidades de backup hot e instantâneo.  
  
## Permissões  
 O Serviço Gravador do SQL deve ser executado na conta **Sistema Local**. O Serviço Gravador do SQL usa o logon **NT Service\SQLWriter** para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O uso do logon **NT Service\SQLWriter** permite que o processo do Gravador do SQL seja executado no nível mais baixo de privilégio em uma conta designada como **nenhum logon**, que limita a vulnerabilidade. Se o serviço do Gravador do SQL estiver desabilitado, qualquer utilitário que confie em instantâneos do VSS, como o System Center Data Protection Manager, bem como em outros produtos de terceiros, será interrompido, ou pior, correrá o risco de obter backups de bancos de dados que não estavam consistentes. Se nem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o sistema em que é executado, nem o sistema host (no caso de uma máquina virtual), precisarem usar qualquer coisa além do backup de [!INCLUDE[tsql](../../includes/tsql-md.md)], o serviço do Gravador do SQL poderá seguramente ser desabilitado e o logon será removido.  Observe que o serviço do Gravador do SQL pode ser chamado por um backup em nível de sistema ou de volume, seja o backup diretamente baseado em instantâneo ou não. Alguns produtos de backup de sistema usam o VSS para evitar serem bloqueados por arquivos abertos ou bloqueados. O Serviço Gravador do SQL precisa de permissões elevadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pois, no decorrer de suas atividades, ele congelará brevemente qualquer E/S para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Recursos  
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
  
  