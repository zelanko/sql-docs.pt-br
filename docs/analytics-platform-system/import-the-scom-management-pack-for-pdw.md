---
title: Importar o pacote de gerenciamento do SCOM - Analytics Platform System | Microsoft Docs
description: Siga estas etapas para importar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o Analytics Platform System (APS). Os pacotes de gerenciamento necessários para monitorar o Parallel Data Warehouse do SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e60d87ae58b0804a0a7296f8b489df7441683c5b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importar o pacote de gerenciamento do SCOM - Analytics Platform System
Siga estas etapas para importar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o Analytics Platform System (APS). Os pacotes de gerenciamento necessários para monitorar o Parallel Data Warehouse do SCOM. 
  
## <a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager 2007 R2 deve ser instalado e em execução.  
  
Os pacotes de gerenciamento devem ser instalados. Consulte [instalar os pacotes de gerenciamento do SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md).  
  
## <a name="Step1"></a>Etapa 1: Importar o pacote de gerenciamento de Base de dispositivo do SQL Server  
  
1.  Faça logon no computador com uma conta que seja membro da função administradores do Operations Manager para o grupo de gerenciamento do Operations Manager 2007.  
  
2.  No console de operações, clique em **administração**.  
  
3.  Clique com botão direito do **pacotes de gerenciamento** nó e, em seguida, clique **importar pacotes de gerenciamento**.  
  
    ![Clique em Importar pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM")  
  
4.  Na lista de pacotes de gerenciamento, selecione o pacote de gerenciamento que você deseja importar, clique em **selecione**e, em seguida, clique em **adicionar**.  
  
    ![Lista de pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Procurar **dispositivo** e, depois, detalhar Base de dispositivo do SQL Server e, em seguida, clique em **adicionar** as duas opções.  
  
    ![Base de aplicativo do SQL Server](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Depois que os dois pacotes de gerenciamento foram no painel inferior selecionado, clique em **Okey**.  
  
    ![Selecione os pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Clique em **Instalar**.  
  
    ![Clique em instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Uma vez concluído, clique em **fechar**.  
  
    ![Uma vez concluído, clique em Fechar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Importar o pacote de monitoramento para Microsoft SQL Server 2008 R2 Parallel Data Warehouse Appliance  
  
1.  Clique com botão direito do **pacotes de gerenciamento** nó e, em seguida, clique **importar pacotes de gerenciamento**.  
  
2.  Escolha **adicionar do disco**...  
  
    ![Clique com botão direito pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Vá para o local onde você extraiu os pacotes de gerenciamento do SQL Server PDW e escolha os três pacotes de gerenciamento que estão na seção "Pacotes de gerenciamento selecionado para importar". Você pode fazer isso selecionando o primeiro, clicando em Shift e selecionando o último deles. Depois que todas elas estão selecionadas, clique em **abrir**.  
  
    ![Selecione pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Clique em **Instalar**.  
  
    ![Clique em instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Clique em **Fechar**.  
  
    ![Clique em Fechar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você importou os pacotes de gerenciamento, prossiga para a próxima etapa: [configurar o SCOM para monitorar Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
