---
title: "Mesclar Conflitos (Suplemento MDS para Excel) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf95978f-a2c5-4325-8606-dbd4e88741b8
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Mesclar Conflitos (Suplemento MDS para Excel)
  No Suplemento [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para Excel, se os dados tiverem sido alterados por outro usuário, a publicação falhará com um erro de conflito. Para resolver esse erro, você pode executar conflitos de mesclagem e republicar as alterações.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão Atualizar para o objeto de modelo folha para a entidade que você está atualizando.  
  
-   A planilha ativa deve ter dados gerenciados por MDS.  
  
-   A planilha ativa deve ter um erro de conflito após uma tentativa de publicar as alterações.  
  
### Para mesclar conflitos  
  
1.  Na planilha, selecione a linha ou célula que contém o erro de conflito.  
  
2.  No grupo de menus **Publicar e Validar** , escolha **Mesclar Conflitos** para abrir a caixa de diálogo **Mesclar Conflitos** .  
  
3.  Na caixa de diálogo **Mesclar Conflitos** , você pode:  
  
    -   Escolha **Mais recente** e clique em **Aplicar** para desfazer as alterações pendentes e recarregar a versão mais recente a partir do servidor.  
  
    -   Escolher **Original** e clicar em **Aplicar** para aplicar a versão original à planilha.  
  
    -   Escolher **Sua** e clicar em **Aplicar** para manter as alterações locais existentes.  
  
4.  Depois de clicar em **Aplicar**, você poderá fazer alterações adicionais e publicar novamente. Ou você pode clicar em **Cancelar** para cancelar a atualização e a recarga da versão mais recente do servidor.  
  
## Consulte também  
 [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  