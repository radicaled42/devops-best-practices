# Sample Terraform playbook


```
provider "aws" {
  region = "us-west-2"  # Change to your desired region
}

resource "aws_kms_key" "s3_kms_key" {
  description             = "KMS key for S3 encryption"
  deletion_window_in_days = 10

  tags = {
    Name        = "S3KmsKey"
    Environment = "Production"
  }
}

resource "aws_kms_alias" "s3_kms_alias" {
  name          = "alias/s3kmskey"
  target_key_id = aws_kms_key.s3_kms_key.id
}

resource "aws_s3_bucket" "s3_bucket" {
  bucket = "my-s3-bucket"  # Change to your desired bucket name

  tags = {
    Name        = "MyBucket"
    Environment = "Production"
  }

  server_side_encryption_configuration {
    rule {
      apply_server_side_encryption_by_default {
        sse_algorithm   = "aws:kms"
        kms_master_key_id = aws_kms_key.s3_kms_key.arn
      }
    }
  }
}

output "bucket_name" {
  value = aws_s3_bucket.s3_bucket.bucket
}
```