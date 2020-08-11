---
title: Implementando uma classe DataReader para uma extensão de processamento de dados | Microsoft Docs
description: Aumente o desempenho do aplicativo e reduza a sobrecarga do sistema implementando uma classe DataReader para uma extensão de processamento de dados.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1fbbf2e31b32cf8f4573da7281caeec97af7840d
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529996"
---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>Implementando uma classe DataReader para uma extensão de processamento de dados
  O objeto **DataReader** permite que um cliente recupere um fluxo de dados somente leitura, somente encaminhamento de uma fonte de dados. Os resultados são retornados à medida que a consulta é executada e são armazenados no buffer de rede no cliente até que você solicite-os usando o método **Read** da classe **DataReader**. Para criar uma classe **DataReader**, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> e, opcionalmente, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>. O uso de um objeto **DataReader** aumenta o desempenho do aplicativo recuperando dados assim que eles estão disponíveis, em vez de aguardar que todos os resultados da consulta sejam retornados e (por padrão) armazenando somente uma linha por vez na memória, reduzindo a sobrecarga do sistema.  
  
 Depois de criar uma instância da classe **Command**, você cria um objeto **DataReader** chamando **Command.ExecuteReader** para recuperar linhas da fonte de dados. A implementação de **DataReader** deve fornecer duas funcionalidades básicas: acesso somente encaminhamento aos conjuntos de resultados obtidos pela execução de um comando e acesso aos tipos de coluna, nomes e valores de cada linha. Os clientes usam o método **Read** do objeto **DataReader** para obter uma linha dos resultados da consulta.  
  
 No Designer de Relatórios, o objeto **DataReader** é usado para recuperar uma lista de campos, além de informações de esquema sobre o conjunto de resultados. Isso é realizado pela implementação dos métodos **GetName**, **GetValue**, **GetFieldType** e **GetOrdinal** da interface <xref:Microsoft.ReportingServices.DataProcessing.IDataReader>.  
  
 A interface de <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> permite que você ofereça informações específicas de agregação sobre o seu conjunto de resultados. Para obter uma implementação de exemplo da classe **DataReader**, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
