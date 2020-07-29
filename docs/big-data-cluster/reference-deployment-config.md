---
title: Arquivo de configuração de implantação
titleSuffix: SQL Server Big Data Clusters
description: Referência para um arquivo de configuração de implantação de cluster de Big Data.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 2/19/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3a94fb34110401c16b81bd05993e2cf85d2fdc5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752111"
---
# <a name="deployment-configuration-file-reference-for-big-data-clusters"></a>Referência do arquivo de configuração de implantação para clusters de Big Data

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo fornece um arquivo JSON que documenta a estrutura de um arquivo de configuração de implantação de cluster de Big Data do SQL Server 2019.

> [!TIP]
> Não use isso como seu arquivo de configuração de implantação real. Em vez disso, siga as instruções nas [diretrizes de implantação](deployment-guidance.md#configfile) para saber como trabalhar com arquivos de configuração.

## <a name="deployment-configuration-file"></a>Arquivo de configuração de implantação

Use o arquivo JSON a seguir como uma referência para a estrutura e as configurações em um arquivo de configuração de implantação de cluster de Big Data.

```json
{
  "apiVersion": {
    "name": "API Version",
    "description": "The API version"
  },
  "metadata": {
    "kind": {
      "name": "Deployment Type",
      "description": "The type of deployment - in this case a 'Cluster'"
    },
    "name": {
      "name": "Cluster Name",
      "description": "SQL Server big data cluster name. This is also the name of the Kubernetes namespace to deploy SQLServer big data cluster into."
    }
  },
  "spec": {
    "resources": [
      {
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "HDFS Name Node"
          },
          "replicas": {
            "name": "HDFS Name Node Replicas",
            "description": "The number of replicas you would like in HDFS Name Node pool"
          },
          "settings": {
            "name": "HDFS Name Node pool configurations",
            "description": "Configuration key-value pairs for HDFS Name Node pool, overriding service configurations"
          }
        }
      },
      {
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Spark Head Node"
          },
          "replicas": {
            "name": "Spark Head Node Replicas",
            "description": "The number of replicas you would like in Spark Head Node pool"
          },
          "settings": {
            "name": "Spark Head Node pool configurations",
            "description": "Configuration key-value pairs for Spark Head Node pool, overriding service configurations"
          }
        }
      },
      {
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Zookeeper"
          },
          "replicas": {
            "name": "Zookeeper Node Replicas",
            "description": "The number of replicas you would like in Zookeeper pool"
          },
          "settings": {
            "name": "Zookeeper Node pool configurations",
            "description": "Configuration key-value pairs for Zookeeper Node pool, overriding service configurations"
          }
        }
      },
      {
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Gateway"
          },
          "replicas": {
            "name": "Gateway Node Replicas",
            "description": "The number of replicas you would like in Gateway pool"
          },
          "settings": {
            "name": "Gateway pool configurations",
            "description": "Configuration key-value pairs for Gateway pool, overriding service configurations"
          },
          "endpoints": [
            {
              "name": {
                "name": "Gateway Endpoint Name",
                "description": "Endpoint name of gateway pool"
              },
              "dnsName": {
                "name": "Gateway DNS Name",
                "description": "External DNS name for gateway pool"
              },
              "serviceType": {
                "name": "Gateway Pool Endpoint Type",
                "description": "Endpoint type of gateway pool - NodePort"
              },
              "port": {
                "name": "Gateway Pool Port",
                "description": "The port for the gateway endpoint"
              }
            }
          ]
        }
      },
      {
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "AppProxy"
          },
          "replicas": {
            "name": "AppProxy Node Replicas",
            "description": "The number of replicas you would like in AppProxy pool"
          },
          "settings": {
            "name": "AppProxy pool configurations",
            "description": "Configuration key-value pairs for AppProxy pool, overriding service configurations"
          },
          "endpoints": [
            {
              "name": {
                "name": "AppProxy Endpoint Name",
                "description": "Endpoint name of appproxy pool"
              },
              "dnsName": {
                "name": "AppProxy DNS Name",
                "description": "External DNS name for appproxy pool"
              },
              "serviceType": {
                "name": "AppProxy Pool Endpoint Type",
                "description": "Endpoint type of appproxy pool - NodePort"
              },
              "port": {
                "name": "AppProxy Pool Port",
                "description": "The port for the appproxy endpoint"
              }
            }
          ]
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Master"
          },
          "replicas": {
            "name": "Master Pool Replicas",
            "description": "The number of replicas you would like in Master pool"
          },
          "settings": {
            "name": "Master pool configurations",
            "description": "Configuration key-value pairs for Master pool, overriding service configurations"
          },
          "storage": {
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "This indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          },
          "endpoints": [
            {
              "name": {
                "name": "Master Endpoint Name",
                "description": "Endpoint name of Master pool"
              },
              "dnsName": {
                "name": "Master DNS Name",
                "description": "External DNS name for Master pool"
              },
              "serviceType": {
                "name": "Master Pool Endpoint Type",
                "description": "Endpoint type of Master Pool - NodePort"
              },
              "port": {
                "name": "Master Pool Port",
                "description": "The port for the master endpoint"
              }
            }
          ]
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Compute"
          },
          "replicas": {
            "name": "Compute Pool Replicas",
            "description": "The number of replicas you would like in Compute pool"
          },
          "settings": {
            "name": "Compute pool configurations",
            "description": "Configuration key-value pairs for Compute pool, overriding service configurations"
          },
          "storage": {
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "This indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          }
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Data"
          },
          "replicas": {
            "name": "Data Pool Replicas",
            "description": "The number of replicas you would like in Data pool"
          },
          "settings": {
            "name": "Data pool configurations",
            "description": "Configuration key-value pairs for Data pool, overriding service configurations"
          },
          "storage": {
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "This indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          }
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Storage"
          },
          "replicas": {
            "name": "Storage Pool Replicas",
            "description": "The number of replicas you would like in Storage pool"
          },
          "settings": {
            "name": "Storage pool configurations",
            "description": "Configuration key-value pairs for Storage pool, overriding service configurations"
          },
          "storage": {
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "This indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          }
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Spark - this is an optional pool that only runs Spark job, it does not run HDFS data node"
          },
          "replicas": {
            "name": "Spark Pool Replicas",
            "description": "The number of replicas you would like in Spark pool"
          },
          "settings": {
            "name": "Spark pool configurations",
            "description": "Configuration key-value pairs for Spark pool, overriding service configurations"
          },
          "storage": {
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "This indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          }
        }
      }
    ],
    "services": {
      "sql": {
        "resources": [
          {
            "name": "Resource",
            "description": "Resource to be included in sql service, includes master, compute, data and storage pool"
          }
        ],
        "settings": {
          "name": "sql service configurations",
          "description": "Configuration key-value pairs for sql service"
        }
      },
      "hdfs": {
        "resources": [
          {
            "name": "Resource",
            "description": "Resource to be included in hdfs service, includes name node, zookeeper, storage and spark head pool, optionally includes spark pool"
          }
        ],
        "settings": {
          "name": "hdfs service configurations",
          "description": "Configuration key-value pairs for hdfs service"
        }
      },
      "spark": {
        "resources": [
          {
            "name": "Resource",
            "description": "Resource to be included in spark service, includes storage and spark head pool, optionally includes spark pool"
          }
        ],
        "settings": {
          "name": "spark service configurations",
          "description": "Configuration key-value pairs for spark service"
        }
      }
    }
  }
}

```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar e personalizar arquivos de configuração de implantação, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md#configfile).
