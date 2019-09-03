# Get AMI IDs per region automatically for your CloudFormation template

In most cases people use Mapping in CloudFormation in order associates AMI IDs with AWS regions as it described [THIS](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html) example.

I know how is it annoying to manually searching for AMI IDs in different AWS regions and build that map by your own, especially if your map is bigger than one image per region. That's why this tool had been created.

## How to use
Let's say there is requirement for only one image per region. Ok, all you need to specify it's AMI ID and an AWS region where it locates.

```
cfn-ami-to-mapping --image-id ami-02f706d959cedf892 --top-level-key AMIID --us-east-2
```
Wait several seconds and you will get your autogenerated block of mapping
```yaml
AMIRegionMap:
  ap-northeast-1:
    AMILinux: ami-04b2d1589ab1d972c
  ap-northeast-2:
    AMILinux: ami-0be3e6f84d3b968cd
  ap-south-1:
    AMILinux: ami-0b99c7725b9484f9e
  ap-southeast-1:
    AMILinux: ami-0fb6b6f9e81056553
  ap-southeast-2:
    AMILinux: ami-075caa3491def750b
  ca-central-1:
    AMILinux: ami-0a67d15f2858e33cb
  eu-central-1:
    AMILinux: ami-026d3b3672c6e7b66
  eu-north-1:
    AMILinux: ami-8c169ef2
  eu-west-1:
    AMILinux: ami-0862aabda3fb488b5
  eu-west-2:
    AMILinux: ami-0bdfa1adc3878cd23
  eu-west-3:
    AMILinux: ami-05b93cd5a1b552734
  sa-east-1:
    AMILinux: ami-0bb96001cf2299257
  us-east-1:
    AMILinux: ami-035b3c7efe6d061d5
  us-east-2:
    AMILinux: ami-02f706d959cedf892
  us-west-1:
    AMILinux: ami-0fcdcdb074d2bac5f
  us-west-2:
    AMILinux: ami-0f2176987ee50226e
```
#### :grey_exclamation: Please, play attention
- You may not specify a region in this case it will use default one which is `us-east-1`. Therefore you need to specify AMI ID of image from `us-east-1`.
- By the default utility creates output using `yaml` format. If you want to change it to `json`, then run the utility with `--json` flag.
```
cfn-ami-to-mapping --image-id ami-02f706d959cedf892 --top-level-key AMIID --us-east-2 --json
```
And the output:
```json
{
    "AMIRegionMap": {
        "ap-northeast-1": {
            "AMILinux": "ami-04b2d1589ab1d972c"
        },
        "ap-northeast-2": {
            "AMILinux": "ami-0be3e6f84d3b968cd"
        },
        "ap-south-1": {
            "AMILinux": "ami-0b99c7725b9484f9e"
        },
        "ap-southeast-1": {
            "AMILinux": "ami-0fb6b6f9e81056553"
        },
        "ap-southeast-2": {
            "AMILinux": "ami-075caa3491def750b"
        },
        "ca-central-1": {
            "AMILinux": "ami-0a67d15f2858e33cb"
        },
        "eu-central-1": {
            "AMILinux": "ami-026d3b3672c6e7b66"
        },
        "eu-north-1": {
            "AMILinux": "ami-8c169ef2"
        },
        "eu-west-1": {
            "AMILinux": "ami-0862aabda3fb488b5"
        },
        "eu-west-2": {
            "AMILinux": "ami-0bdfa1adc3878cd23"
        },
        "eu-west-3": {
            "AMILinux": "ami-05b93cd5a1b552734"
        },
        "sa-east-1": {
            "AMILinux": "ami-0bb96001cf2299257"
        },
        "us-east-1": {
            "AMILinux": "ami-035b3c7efe6d061d5"
        },
        "us-east-2": {
            "AMILinux": "ami-02f706d959cedf892"
        },
        "us-west-1": {
            "AMILinux": "ami-0fcdcdb074d2bac5f"
        },
        "us-west-2": {
            "AMILinux": "ami-0f2176987ee50226e"
        }
    }
}
```