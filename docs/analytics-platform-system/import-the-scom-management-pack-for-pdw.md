---
title: Importar pacote de gerenciamento do SCOM
description: Siga estas etapas para importar os pacotes de gerenciamento System Center Operations Manager (SCOM) para o sistema de plataforma de análise (APS). Os pacotes de gerenciamento são necessários para monitorar data warehouse paralelos do SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bcb0e667424767fd53a5fc7e027e84d512022203
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401079"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importar o pacote de gerenciamento do SCOM – sistema de plataforma de análise
Siga estas etapas para importar os pacotes de gerenciamento System Center Operations Manager (SCOM) para o sistema de plataforma de análise (APS). Os pacotes de gerenciamento são necessários para monitorar data warehouse paralelos do SCOM. 
  
## <a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager 2007 R2 deve estar instalado e em execução.  
  
Os pacotes de gerenciamento devem ser instalados. Confira [instalar os pacotes de gerenciamento do SCOM &#40;o sistema de plataforma de análise&#41;](install-the-scom-management-packs.md).  
  
## <a name="Step1"></a>Etapa 1: importar o pacote de gerenciamento básico do dispositivo SQL Server  
  
1.  Faça logon no computador com uma conta que seja membro da função Administradores do Operations Manager do Grupo de Gerenciamento do Operations Manager 2007.  
  
2.  No console de Operações, clique em **Administração**.  
  
3.  Clique com o botão direito do mouse no nó **pacotes de gerenciamento** e clique em **importar pacotes de gerenciamento**.  
  
    ![Clique em Importar Pacotes de Gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  Na lista de pacotes de gerenciamento, selecione o pacote de gerenciamento que você deseja importar, clique em **selecionar**e, em seguida, clique em **Adicionar**.  
  
    ![Lista de pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Pesquise por **dispositivo** e faça uma busca detalhada na base do dispositivo SQL Server e, em seguida, clique em **Adicionar** as duas opções.  
  
    ![Base de aplicativo do SQL Server](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Depois que os dois pacotes de gerenciamento estiverem no painel inferior selecionado, clique em **OK**.  
  
    ![Selecione os dois pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Clique em **Instalar**.  
  
    ![Clique em instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Após a conclusão, clique em **fechar**.  
  
    ![Depois de concluir, clique em Fechar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Importar o pacote de monitoramento para o Microsoft SQL Server 2008 R2 Parallel data warehouse Appliance  
  
1.  Clique com o botão direito do mouse no nó **pacotes de gerenciamento** e clique em **importar pacotes de gerenciamento**.  
  
2.  Escolha **Adicionar do disco**....  
  
    ![Clique com o botão direito do mouse em Pacotes de Gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Vá para o local onde você extraiu os pacotes de gerenciamento de SQL Server PDW e escolha os três pacotes de gerenciamento que estão na seção "pacotes de gerenciamento selecionados para importação". Você pode fazer isso selecionando a primeira, clicando em Shift e selecionando a última. Quando todos estiverem selecionados, clique em **abrir**.  
  
    ![Selecionar pacotes de gerenciamento](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Clique em **Instalar**.  
  
    ![Clique em instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Clique em **Fechar**.  
  
    ![Clique em fechar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você importou os pacotes de gerenciamento, continue para a próxima etapa: [Configurar o SCOM para monitorar o sistema de plataforma de análise &#40;o sistema de plataforma de análise&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
