# Setup

All of the examples below can be easily reproduced by launching a fake EC2 instance against a moto backend:

```bash
$ docker run --rm -it -p 5000:5000 --name moto_backend -d motoserver/moto:latest
$ aws ec2 run-instances \
    --image-id ami-0abcdef1234567890 \
    --instance-type t2.micro \
    --key-name MyKeyPair \
    --endpoint-url http://localhost:5000 \
    --region us-east-1
```

# Examples

* [Accessing key](#accessing-key)
* [Accessing value](#accessing-value)
* [Filtering by equality](#filtering-by-equality)
* [Filtering by inequality](#filtering-by-inequality)
* [Filtering by contains](#filtering-by-contains)
* [Filtering by not contains](#filtering-by-not-contains)
* [Filtering by starts with](#filtering-by-starts-with)
* [Filtering by not starts with](#filtering-by-not-starts-with)
* [Filtering by ends with](#filtering-by-ends-with)
* [Filtering by not ends with](#filtering-by-not-ends-with)
* [Filtering by numeric comparison](#filtering-by-numeric-comparison)
* [Filtering by equality with multiple conditions](#filtering-by-equality-with-multiple-conditions)
* [Filtering by inequality with multiple conditions](#filtering-by-inequality-with-multiple-conditions)
* [Filtering by contains with multiple conditions](#filtering-by-contains-with-multiple-conditions)

<br>

# Accessing key

The example shows how to access the `Reservations` key:

```bash
aws ec2 describe-instances --query 'Reservations' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Accessing value

The example shows how to access the `Instances` value:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by equality

The example shows how to filter when the `ImageId` value is equal to `ami-0abcdef1234567890`:


```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?ImageId==`ami-0abcdef1234567890`]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by inequality

The example shows how to filter when the `ImageId` value is not equal to `ami-0abcdef1234567890`:


```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?ImageId!=`ami-0abcdef1234567890`]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by contains

The example shows how to filter when the `ImageId` value contains `0abcdef1234567890`:


```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?contains(ImageId,`0abcdef1234567890`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by not contains

The example shows how to filter when the `ImageId` value does not contain `0abcdef1234567890`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?!contains(ImageId,`0abcdef1234567890`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by starts with

The example shows how to filter when the `ImageId` value starts with `ami-`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?starts_with(ImageId,`ami-`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by not starts with

The example shows how to filter when the `ImageId` value does not start with `ami-`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?!starts_with(ImageId,`ami-`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by ends with

The example shows how to filter when the `ImageId` value ends with `ami-`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?ends_with(ImageId,`ami-`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by not ends with

The example shows how to filter when the `ImageId` value does no end with `ami-`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?!ends_with(ImageId,`ami-`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by numeric comparison

The example shows how to filter when the `Code` value of the `State` property is greater than `15`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?State.Code > `15`]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

The example shows how to filter when the `Code` value of the `State` property is less than `20`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?State.Code < `20`]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by equality with multiple conditions

The example shows how to filter when the `ImageId` value is equal to `ami-0abcdef1234567890` AND `ami-xxx`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?ImageId==`ami-0abcdef1234567890` && ImageId==`ami-xxx`]' --endpoint-url http://localhost:5000 --region us-east-1
```

The example shows how to filter when the `ImageId` value is equal to `ami-0abcdef1234567890` OR `ami-xxx`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?ImageId==`ami-0abcdef1234567890` || ImageId==`ami-xxx`]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by inequality with multiple conditions

The example shows how to filter when the `ImageId` value is not equal to `ami-0abcdef1234567890` OR `ami-xxx`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?ImageId!=`ami-0abcdef1234567890` || ImageId!=`ami-xxx`]' --endpoint-url http://localhost:5000 --region us-east-1
```

The example shows how to filter when the `ImageId` value is not equal to `ami-0abcdef1234567890` AND `ami-xxx`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?ImageId!=`ami-0abcdef1234567890` && ImageId!=`ami-xxx`]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

# Filtering by contains with multiple conditions

The example shows how to filter when the `ImageId` value contains `ami-0abcdef1234567890` OR `foo`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?contains(ImageId,`0abcdef1234567890`) || contains(ImageId, `foo`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

The example shows how to filter when the `ImageId` value contains `ami-0abcdef1234567890` AND `foo`:

```bash
aws ec2 describe-instances --query 'Reservations[].Instances[?contains(ImageId,`0abcdef1234567890`) && contains(ImageId, `foo`)]' --endpoint-url http://localhost:5000 --region us-east-1
```

<br>

