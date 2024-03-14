# terraform-aws-autoscaling-schedule
Implements scheduled scaling for AWS Auto Scaling described here : https://docs.aws.amazon.com/autoscaling/application/userguide/application-auto-scaling-scheduled-scaling.html

Use the 'aws_autoscaling_schedule' terraform resource : https://www.terraform.io/docs/providers/aws/r/autoscaling_schedule.html

# Usage example
```
module "autoscaling-schedule" {
  source  = "github.com/santhoshbhandari3008/terraform-aws-autoscaling-schedule"
  version = "1.0.0"

  asg_schedules = {
    "startup" = {
      min_size          = "1",
      max_size          = "0",
      desired_capacity  = "1",
      recurrence        = "30 5 * * MON-FRI",
      asg_name          = [ "rfidprod.int-blue", "rfidprod.int-green" ],
      time_zone         = "Etc/UTC"
    },
    "shutdown" = {
      min_size          = "0",
      max_size          = "0",
      desired_capacity  = "0",
      recurrence        = "0 18 * * MON-FRI",
      asg_name          = [ "rfidprod.int-blue", "rfidprod.int-green" ],
      time_zone         = "Etc/UTC"
    }
  }
}
```
