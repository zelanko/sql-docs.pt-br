---
title: Instalar pacotes de gerenciamento do SCOM
description: Siga estas etapas para baixar e instalar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para SQL Server PDW. Os pacotes de gerenciamento são necessários para monitorar SQL Server PDW do SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 0db3a588dfabf290f2e095adafcd3331187af957
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766975"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Instalar os pacotes de gerenciamento do SQL Server Operations Manager (SCOM) para o Analytics Platform System
Siga estas etapas para baixar e instalar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para SQL Server PDW. Os pacotes de gerenciamento são necessários para monitorar SQL Server PDW do SCOM.  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager deve estar instalado e em execução. SQL Server PDW 2012 requer System Center Operations Manager 2007 R2, System Center Operations Manager 2012 ou System Center Operations Manager 2012 service pack 1.  
  
## <a name="step-1-download-the-management-packs"></a><a name="Step1"></a>Etapa 1: baixar os pacotes de gerenciamento  
Para a carga de trabalho de PDW do APS, baixe o [pacote de gerenciamento do System Center para o Microsoft Analytics Platform System](https://go.microsoft.com/fwlink/?LinkId=396857).  
  
Para o gerenciamento de dispositivos, baixe o [pacote de gerenciamento básico do dispositivo SQL Server](/previous-versions/system-center/packs/gg602398(v=technet.10)).  
  
Para versões mais antigas do PDW sem APS, baixe o[pacote de monitoramento do System Center para Microsoft SQL Server dispositivo de data warehouse paralela 2012](https://go.microsoft.com/fwlink/p/?LinkId=282661).  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="step-2-install-the-management-packs"></a><a name="Step2"></a>Etapa 2: instalar os pacotes de gerenciamento  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>Instalar o pacote de gerenciamento básico do dispositivo SQL Server  
  
1.  Para executar a instalação, clique duas vezes no pacote de gerenciamento básico do dispositivo SQL Server baixado.  
  
2.  Aceite o contrato de licença e clique em **Avançar**.  
  
    ![Aceitar o contrato de licença](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  Selecione sua própria pasta de instalação ou use a pasta de instalação padrão do pacote de gerenciamento.  
  
    ![Selecionar pasta de instalação](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  Clique em **Instalar**.  
  
    ![Confirmar a instalação](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  Clique em **fechar**  
  
    ![Clique em fechar](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>Instalar o pacote de monitoramento para o dispositivo SQL Server PDW  
  
1.  Para executar a instalação, clique duas vezes no pacote de gerenciamento do dispositivo baixado SQL Server PDW.  
  
2.  Aceite o contrato de licença e clique em **Avançar**.  
  
    ![Aceitar o contrato de licença](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  Escolha o diretório que irá conter os arquivos extraídos. A pasta de instalação padrão do pacote de gerenciamento é mostrada por padrão. Selecione o padrão ou selecione sua própria pasta de instalação.  
  
    ![Selecionar pasta de instalação](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  Clique em **Instalar**.  
  
    ![Confirmar a instalação](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  Clique em **fechar**  
  
    ![Instalação concluída](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você tem os pacotes de gerenciamento instalados, vá para a próxima etapa: [importar o pacote de gerenciamento do SCOM para o PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
