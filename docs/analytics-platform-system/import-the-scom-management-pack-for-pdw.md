---
title: Importar pacote de gerenciamento do SCOM - Analytics Platform System | Microsoft Docs
description: Siga estas etapas para importar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o Analytics Platform System (APS). Os pacotes de gerenciamento necessários para monitorar o Parallel Data Warehouse do SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 070e7b73614f6884e45a5c91603d6086613d15ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960854"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importar o pacote de gerenciamento do SCOM - Analytics Platform System
Siga estas etapas para importar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o Analytics Platform System (APS). Os pacotes de gerenciamento necessários para monitorar o Parallel Data Warehouse do SCOM. 
  
## <a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager 2007 R2 deve ser instalado e em execução.  
  
Os pacotes de gerenciamento devem ser instalados. Ver [instalar os pacotes de gerenciamento do SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md).  
  
## <a name="Step1"></a>Etapa 1: Importar o pacote de gerenciamento Base do SQL Server Appliance  
  
1.  Faça logon no computador com uma conta que seja um membro da função administradores do Operations Manager para o grupo de gerenciamento do Operations Manager 2007.  
  
2.  No console de operações, clique em **administração**.  
  
3.  Clique com botão direito do **pacotes de gerenciamento** nó e clique **importar pacotes de gerenciamento**.  
  
    ![Clique em Importar pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM")  
  
4.  Na lista de pacotes de gerenciamento, selecione o pacote de gerenciamento que você deseja importar, clique em **selecionar**e, em seguida, clique em **Add**.  
  
    ![Lista de pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Pesquise **Appliance** e, em seguida, fazer uma busca detalhada na Base de dispositivo do SQL Server e, em seguida, clique em **Add** as duas opções.  
  
    ![Base de aplicativo do SQL Server](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Depois que os dois pacotes de gerenciamento foram no painel inferior selecionado, clique em **Okey**.  
  
    ![Selecione os dois pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Clique em **Instalar**.  
  
    ![Clique em instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Uma vez concluído, clique em **fechar**.  
  
    ![Uma vez concluído, clique em Fechar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Importar o pacote de monitoramento para Microsoft SQL Server 2008 R2 Parallel Data Warehouse Appliance  
  
1.  Clique com botão direito do **pacotes de gerenciamento** nó e clique **importar pacotes de gerenciamento**.  
  
2.  Escolher **adicionar do disco**...  
  
    ![Pacotes de gerenciamento com o botão direito](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Vá para o local onde você extraiu os pacotes de gerenciamento do SQL Server PDW e escolha os três pacotes de gerenciamento que estão na seção "Pacotes de gerenciamento selecionado para importar". Você pode fazer isso selecionando o primeiro, em Shift e selecionar o último deles. Depois que todos eles são selecionados, clique em **aberto**.  
  
    ![Selecione pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Clique em **Instalar**.  
  
    ![Clique em instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Clique em **Fechar**.  
  
    ![Click Close](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você importou os pacotes de gerenciamento, continue para a próxima etapa: [Configurar o SCOM para monitorar o Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
